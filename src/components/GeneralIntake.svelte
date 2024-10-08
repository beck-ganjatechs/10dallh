<script lang="ts">
  import { navigate } from "svelte-routing";
  import { gsap } from "gsap";
  import { onMount } from "svelte";
  import PocketBase from 'pocketbase';

  let medicalConditions = "";
  let medications = "";
  let idDocument: File | null = null;

  const pb = new PocketBase('http://127.0.0.1:8090');

  onMount(() => {
    gsap.from("form", { opacity: 0, y: 50, duration: 1 });
  });

  async function handleSubmit() {
    try {
      const formData = new FormData();
      formData.append('medicalConditions', medicalConditions);
      formData.append('medications', medications);
      if (idDocument) {
        formData.append('idDocument', idDocument);
      }

      await pb.collection('general_intake').create(formData);
      navigate("/checkout");
    } catch (error) {
      console.error("Error submitting general intake:", error);
    }
  }
</script>

<form on:submit|preventDefault={handleSubmit}>
  <h2>General Intake Questions</h2>
  
  <textarea bind:value={medicalConditions} placeholder="Do you have any medical conditions?" rows="4"></textarea>
  <textarea bind:value={medications} placeholder="Are you taking any medications?" rows="4"></textarea>
  
  <div>
    <label for="id-upload">Upload ID for verification:</label>
    <input id="id-upload" type="file" accept="image/*,.pdf" on:change={(e) => idDocument = e.target.files[0]}>
  </div>
  
  <button type="submit">Submit</button>
</form>

<style>
  form {
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }

  textarea, input, button {
    padding: 0.5rem;
    font-size: 1rem;
  }
</style>
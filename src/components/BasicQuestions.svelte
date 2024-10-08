<script lang="ts">
  import { navigate } from "svelte-routing";
  import { gsap } from "gsap";
  import { onMount } from "svelte";
  import PocketBase from 'pocketbase';

  let dateOfBirth = "";
  let gender = "";
  let address = "";
  let zipCode = "";
  let preferredContactMethod = "";

  const pb = new PocketBase('http://127.0.0.1:8090');

  onMount(() => {
    gsap.from("form", { opacity: 0, y: 50, duration: 1 });
  });

  async function handleSubmit() {
    try {
      const data = {
        dateOfBirth,
        gender,
        address,
        zipCode,
        preferredContactMethod,
      };

      await pb.collection('basic_info').create(data);
      navigate("/store");
    } catch (error) {
      console.error("Error submitting basic info:", error);
    }
  }
</script>

<form on:submit|preventDefault={handleSubmit}>
  <h2>Please answer the following questions:</h2>
  
  <input type="date" bind:value={dateOfBirth} placeholder="Date of Birth" required>
  
  <select bind:value={gender} required>
    <option value="">Select Gender</option>
    <option value="male">Male</option>
    <option value="female">Female</option>
    <option value="other">Other</option>
  </select>
  
  <input type="text" bind:value={address} placeholder="Address" required>
  <input type="text" bind:value={zipCode} placeholder="Zip Code" required>
  
  <select bind:value={preferredContactMethod} required>
    <option value="">Preferred Contact Method</option>
    <option value="phone">Phone</option>
    <option value="email">Email</option>
  </select>
  
  <button type="submit">Submit</button>
</form>

<style>
  form {
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }

  input, select, button {
    padding: 0.5rem;
    font-size: 1rem;
  }
</style>
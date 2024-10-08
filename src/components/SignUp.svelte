<script lang="ts">
  import { navigate } from "svelte-routing";
  import { gsap } from "gsap";
  import { onMount } from "svelte";
  import PocketBase from 'pocketbase';

  let firstName = "";
  let lastName = "";
  let email = "";
  let phoneNumber = "";
  let password = "";

  const pb = new PocketBase('http://127.0.0.1:8090');

  onMount(() => {
    gsap.from("form", { opacity: 0, y: 50, duration: 1 });
  });

  async function handleSignUp() {
    try {
      const data = {
        firstName,
        lastName,
        email,
        phoneNumber,
        password,
        passwordConfirm: password,
      };

      await pb.collection('users').create(data);
      navigate("/how-it-works");
    } catch (error) {
      console.error("Error signing up:", error);
    }
  }

  function handleSocialSignUp(provider: string) {
    // Implement social sign-up logic here
    console.log(`Sign up with ${provider}`);
  }
</script>

<form on:submit|preventDefault={handleSignUp}>
  <h2>Sign Up</h2>
  <button type="button" on:click={() => handleSocialSignUp("Google")}>Sign up with Google</button>
  <button type="button" on:click={() => handleSocialSignUp("Facebook")}>Sign up with Facebook</button>
  
  <input type="text" bind:value={firstName} placeholder="First Name" required>
  <input type="text" bind:value={lastName} placeholder="Last Name" required>
  <input type="email" bind:value={email} placeholder="Email" required>
  <input type="tel" bind:value={phoneNumber} placeholder="Phone Number" required>
  <input type="password" bind:value={password} placeholder="Password" required>
  
  <button type="submit">Sign Up</button>
  
  <p>Already have an account? <a href="/login">Login</a></p>
</form>

<style>
  form {
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }

  input, button {
    padding: 0.5rem;
    font-size: 1rem;
  }
</style>
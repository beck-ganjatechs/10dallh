<script lang="ts">
  import { gsap } from "gsap";
  import { onMount } from "svelte";
  import PocketBase from 'pocketbase';

  let billingAddress = "";
  let cardNumber = "";
  let expirationDate = "";
  let cvv = "";

  const pb = new PocketBase('http://127.0.0.1:8090');

  onMount(() => {
    gsap.from("form", { opacity: 0, y: 50, duration: 1 });
  });

  async function handlePayment() {
    try {
      const data = {
        billingAddress,
        cardNumber,
        expirationDate,
        cvv,
      };

      await pb.collection('payments').create(data);
      alert("Payment successful! Your consultation request has been submitted.");
    } catch (error) {
      console.error("Error processing payment:", error);
    }
  }
</script>

<form on:submit|preventDefault={handlePayment}>
  <h2>Check Out</h2>
  
  <input type="text" bind:value={billingAddress} placeholder="Billing Address" required>
  <input type="text" bind:value={cardNumber} placeholder="Card Number" required>
  <input type="text" bind:value={expirationDate} placeholder="Expiration Date (MM/YY)" required>
  <input type="text" bind:value={cvv} placeholder="CVV" required>
  
  <button type="submit">Pay $10.00</button>
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
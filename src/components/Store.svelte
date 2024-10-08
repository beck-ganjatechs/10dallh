<script lang="ts">
  import { navigate } from "svelte-routing";
  import { gsap } from "gsap";
  import { onMount } from "svelte";

  onMount(() => {
    gsap.from(".product", { opacity: 0, y: 50, duration: 1 });
  });

  function handleSubmit() {
    navigate("/general-intake");
  }
</script>

<div class="store">
  <div class="product">
    <h2>Product: Doctor Evaluation</h2>
    <p>Price: $10.00</p>
    <button on:click={handleSubmit}>Submit</button>
  </div>
</div>

<style>
  .store {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
  }

  .product {
    text-align: center;
    padding: 2rem;
    border: 1px solid #ccc;
    border-radius: 8px;
  }

  button {
    padding: 0.5rem 1rem;
    font-size: 1rem;
  }
</style>
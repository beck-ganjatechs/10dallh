<script lang="ts">
  import { navigate } from "svelte-routing";
  import { gsap } from "gsap";
  import { onMount } from "svelte";

  let name = "User"; // This should be fetched from the user's session

  onMount(() => {
    gsap.from(".content", { opacity: 0, y: 50, duration: 1, stagger: 0.2 });
  });

  function handleNext() {
    navigate("/basic-questions");
  }
</script>

<div class="how-it-works">
  <h2 class="content">Hey {name},</h2>
  
  <div class="content">
    <h3>How it Works</h3>
    <ol>
      <li>Answer a few basic questions about yourself.</li>
      <li>Select the type of medical consultation needed.</li>
      <li>Your information will be reviewed by a healthcare provider who will send your treatment plan.</li>
    </ol>
  </div>
  
  <button class="content" on:click={handleNext}>Next</button>
</div>

<style>
  .how-it-works {
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }

  ol {
    padding-left: 1.5rem;
  }

  button {
    align-self: flex-start;
    padding: 0.5rem 1rem;
    font-size: 1rem;
  }
</style>
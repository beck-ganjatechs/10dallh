<script lang="ts">
  import { Router, Route } from "svelte-routing";
  import SignUp from "./components/SignUp.svelte";
  import HowItWorks from "./components/HowItWorks.svelte";
  import BasicQuestions from "./components/BasicQuestions.svelte";
  import Store from "./components/Store.svelte";
  import GeneralIntake from "./components/GeneralIntake.svelte";
  import Checkout from "./components/Checkout.svelte";

  export let url = "";
</script>

<Router {url}>
  <main>
    <Route path="/" component={SignUp} />
    <Route path="/how-it-works" component={HowItWorks} />
    <Route path="/basic-questions" component={BasicQuestions} />
    <Route path="/store" component={Store} />
    <Route path="/general-intake" component={GeneralIntake} />
    <Route path="/checkout" component={Checkout} />
  </main>
</Router>

<style>
  main {
    max-width: 800px;
    margin: 0 auto;
    padding: 2rem;
  }
</style>
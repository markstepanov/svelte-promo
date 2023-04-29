<script>
  import Router from "svelte-spa-router";
  import Greeting from "./routes/Greeting.svelte";
  import Game from "./routes/Game.svelte";
  import Card from "../components/Card.svelte";

  let routes = {
    "/": Greeting,
    "/game" : Game,
    "/card": Card
  }
</script>

<svelte:head>
</svelte:head>

<main id="main">
  <Router {routes}/>
</main>
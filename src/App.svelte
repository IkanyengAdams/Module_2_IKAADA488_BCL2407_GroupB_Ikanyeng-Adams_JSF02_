<script>
  import Router from "svelte-spa-router";
  import Navbar from "./lib/Navbar.svelte";
  import ProductList from "./lib/ProductList.svelte";
  


  let routes = {
    "/": ProductList,
    
  };
</script>

<Navbar />


<main>
  <Router {routes} />
</main>

<style>

</style>

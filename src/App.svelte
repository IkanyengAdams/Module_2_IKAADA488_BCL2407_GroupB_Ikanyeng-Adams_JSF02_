<script>
  import Router from "svelte-spa-router";
  import Navbar from "./lib/Navbar.svelte";
  import ProductList from "./lib/ProductList.svelte";
  import ProductDetails from "./lib/ProductDetails.svelte";


  let routes = {
    "/": ProductList,
    "/product/:id": ProductDetails
  };
</script>

<Navbar />


<main>
  <Router {routes} />
</main>

<style>

</style>

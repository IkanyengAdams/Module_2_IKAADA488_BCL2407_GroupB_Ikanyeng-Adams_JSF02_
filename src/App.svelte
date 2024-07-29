<script>
  import Router from "svelte-spa-router";
  import Navbar from "./routes/Navbar.svelte";
  import ProductList from "./routes/ProductList.svelte";
  import ProductDetails from "./routes/ProductDetails.svelte";


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

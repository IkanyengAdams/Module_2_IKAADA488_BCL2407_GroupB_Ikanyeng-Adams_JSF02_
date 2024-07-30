<script>
  import Router from "svelte-spa-router";
  import Navbar from "./routes/Navbar.svelte";
  import ProductList from "./routes/ProductList.svelte";
  import ProductDetails from "./routes/ProductDetails.svelte";
  import Cart from "./routes/Cart.svelte";
  import Wishlist from "./routes/Wishlist.svelte";
  import Login from "./routes/Login.svelte";


  let routes = {
    "/": ProductList,
    "/product/:id": ProductDetails,
    '/wishlist': Wishlist,
    '/cart': Cart,
    '/login': Login
  };
</script>

<Navbar />


<main>
  <Router {routes} />
</main>

<style>

</style>

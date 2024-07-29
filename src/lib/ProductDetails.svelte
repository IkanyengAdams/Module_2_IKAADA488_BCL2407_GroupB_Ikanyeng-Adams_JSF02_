<script>
  import { onMount } from 'svelte';
  import { wrap } from 'svelte-spa-router/wrap';

  export let params;

  let product = {};
  let loading = true;

  onMount(async () => {
    try {
      const productResponse = await fetch(`https://fakestoreapi.com/products/${params.id}`);
      product = await productResponse.json();
    } catch (error) {
      console.error('Error fetching data:', error);
    } finally {
      loading = false;
    }
  });
</script>

<style>
  
</style>

{#if loading}
  <p>Loading...</p>
{:else}
  <div class="product-details">
    <img src={product.image} alt={product.title} />
    <h1>{product.title}</h1>
    <p>{product.description}</p>
    <p>{'$' + product.price}</p>
    <div class="rating">
      {#each Array(5) as _, i}
        <svg class={i < Math.round(product.rating.rate) ? 'filled' : 'empty'} viewBox="0 0 24 24">
          <path d="M12 .587l3.668 7.571 8.332 1.151-6.063 5.852 1.428 8.287L12 18.897l-7.365 3.851 1.428-8.287-6.063-5.852 8.332-1.151z"/>
        </svg>
      {/each}
    </div>
  </div>
{/if}

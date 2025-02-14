<script>
  import { onMount } from 'svelte';
  import { push } from 'svelte-spa-router'; //programmatically navigate to different routes within my Svelte application

  /**
   * @typedef {Object} Params
   * @property {string} id - The ID of the product
   */

  /**
   * Parameters passed to the component, including the product ID
   * @type {Params}
   */

  export let params;

  /**
   * @type {Object} product - The product details fetched from the API
   */

  let product = {};

   /**
   * @type {boolean} loading - Indicates whether the product details are still being loaded
   */

  let loading = true;

  /**
   * Fetches the product details from the API using the provided product ID
   */

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

  /**
   * Navigates back to the products list page
   */

  const goBack = () => {
    push('/');
  };
</script>

<style>
  .product-details {
    max-width: 600px;
    height: 700px;
    margin: 2rem auto;
    padding: 1rem;
    border-radius: 8px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
    background-color: white;
  }

  .product-details img {
    height: 200px;
    max-width: 100%;
    border-radius: 8px;
  }

  .product-details h1 {
    font-size: 2rem;
    margin-bottom: 1rem;
  }

  .product-details p {
    font-size: 1rem;
    margin-bottom: 1rem;
  }

  .rating {
    display: flex;
    height: 20px;
  }

  .rating svg.filled {
    fill: #fbc02d;
  }

  .rating svg.empty {
    fill: #e0e0e0;
  }

  .rating span {
    margin-left: 0.5rem;
    font-size: 1rem;
  }

  .back-button {
    margin-top: 1rem;
    padding: 0.5rem 1rem;
    background-color: #3b82f6;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.2s ease-in-out;
  }

  .back-button:hover {
    background-color: #2563eb;
  }
</style>
<!-- initial loading state -->
{#if loading}
  <p>Loading...</p>
{:else}
  <div class="product-details">
    <!-- Displays product image -->
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
      <span>({product.rating.count} reviews)</span>
    </div>
    <!-- Button to navigate back to the products list -->
    <button class="back-button" on:click={goBack}>Back to Products</button>
  </div>
{/if}

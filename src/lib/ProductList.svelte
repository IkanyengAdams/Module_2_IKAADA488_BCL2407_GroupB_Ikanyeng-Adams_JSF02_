<script>
  import { onMount } from 'svelte';

  let products = [];
  let loading = true;

  onMount(async () => {
    try {
      const productsResponse = await fetch('https://fakestoreapi.com/products');
      products = await productsResponse.json();
    } catch (error) {
      console.error('Error fetching data:', error);
    } finally {
      loading = false;
    }
  });

  const viewProduct = (productId) => {
    console.log(`View product with ID: ${productId}`);
  };
</script>

<style>
  body {
    background-color: rgb(10, 17, 19);
    margin: 0;
    font-family: Arial, sans-serif;
  }

  .products-container {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
  }

  .product-card {
    background-color: white;
    border-radius: 8px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
    margin: 1rem;
    padding: 1rem;
    width: calc(25% - 2rem);
    box-sizing: border-box;
    text-align: center;
    transition: transform 0.2s ease-in-out;
  }

  .product-card:hover {
    transform: scale(1.05);
  }

  .product-card img {
    max-width: 100%;
    height: 200px;
    border-radius: 8px;
  }

  .product-card .rating {
    margin-top: 0.5rem;
    display: flex;
    height: 20px;
    justify-content: center;
  }

  .rating svg.filled {
    fill: #fbc02d; 
  }

  .rating svg.empty {
    fill: #e0e0e0; 
  }

  .view-button {
    margin-top: 1rem;
    padding: 0.5rem 1rem;
    background-color: #3b82f6;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.2s ease-in-out;
  }

  .view-button:hover {
    background-color: #2563eb;
  }
</style>

<main>
  {#if loading}
    <p>Loading...</p>
  {:else}
    <div class="products-container">
      {#each products as product}
        <div class="product-card">
          <img src={product.image} alt={product.title} />
          <h2>{product.title}</h2>
          <p>{'$' + product.price}</p>
          <p>{product.category}</p>
          <div class="rating">
            {#each Array(5) as _, i}
              <svg class={i < Math.round(product.rating.rate) ? 'filled' : 'empty'} viewBox="0 0 24 24">
                <path d="M12 .587l3.668 7.571 8.332 1.151-6.063 5.852 1.428 8.287L12 18.897l-7.365 3.851 1.428-8.287-6.063-5.852 8.332-1.151z"/>
              </svg>
            {/each}
          </div>
          <button class="view-button" on:click={() => viewProduct(product.id)}>View Product</button>
        </div>
      {/each}
    </div>
  {/if}
</main>

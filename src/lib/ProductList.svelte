<script>
  import { onMount } from 'svelte';
  import { push } from 'svelte-spa-router';

  let products = [];
  let filteredProducts = [];
  let loading = true;
  let categories = ["Jewellery", "Men's Clothes", "Women's Clothes", "Electronics"];
  let selectedCategory = '';
  let searchQuery = '';

  onMount(async () => {
    try {
      const productsResponse = await fetch('https://fakestoreapi.com/products');
      products = await productsResponse.json();
      filteredProducts = products;
    } catch (error) {
      console.error('Error fetching data:', error);
    } finally {
      loading = false;
    }
  });

  const viewProduct = (productId) => {
    push(`/product/${productId}`);
  };

  const filterProducts = () => {
    filteredProducts = products.filter(product => 
      (!selectedCategory || product.category.includes(selectedCategory)) &&
      (!searchQuery || product.title.toLowerCase().includes(searchQuery.toLowerCase()))
    );
  };

  const searchProducts = () => {
    filterProducts();
  };

  $: filterProducts();
</script>

<style>
  body {
    background-color: rgb(10, 17, 19);
    margin: 0;
    font-family: Arial, sans-serif;
  }

  .container {
    display: flex;
    gap: 1rem;
    justify-content: center;
    margin-top: 1rem;
    align-items: center;
    flex-wrap: wrap;
  }

  .form-group {
    display: flex;
    width: 100%;
    max-width: 31.25rem;
    position: relative;
  }

  .category-select, .search-input, .search-button, .sort-select {
    padding: 0.625rem;
    font-size: 0.875rem;
    border: 1px solid #ccc;
    border-radius: 0.375rem;
  }

  .category-select {
    flex-shrink: 0;
    z-index: 10;
    background-color: #f3f4f6;
    border-radius: 0.375rem 0 0 0.375rem;
  }

  .search-input {
    width: 100%;
    background-color: #f9fafb;
    border-left: 0;
  }

  .search-button {
    position: absolute;
    margin-right: 30px;
    top: 0;
    right: 0;
    height: 100%;
    background-color: #3b82f6;
    color: white;
    border-left: 0;
    border-radius: 0 0.375rem 0.375rem 0;
  }

  .sort-group {
    display: flex;
    align-items: center;
  }

  .sort-label {
    margin-right: 0.5rem;
    font-weight: 600;
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
    <div class="container">
      <div class="form-group">
        <select bind:value="{selectedCategory}" on:change="{filterProducts}" class="category-select">
          <option value="">All Categories</option>
          {#each categories as category}
            <option value="{category}">{category}</option>
          {/each}
        </select>

        <div class="relative w-full">
          <input type="search" class="search-input" placeholder="Search products..." bind:value="{searchQuery}" on:input="{searchProducts}" />
          <button type="submit" class="search-button">
            <svg class="w-4 h-4" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 20 20">
              <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="m19 19-4-4m0-7A7 7 0 1 1 1 8a7 7 0 0 1 14 0Z" />
            </svg>
            <span class="sr-only">Search</span>
          </button>
        </div>
      </div>

      <div class="sort-group">
        <label for="sort" class="sort-label">Sort by</label>
        <select id="sort" class="sort-select">
          <option value="default">Default</option>
          <option value="low">Price: Low to High</option>
          <option value="high">Price: High to Low</option>
        </select>
      </div>
    </div>

    <div class="products-container">
      {#each filteredProducts as product}
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

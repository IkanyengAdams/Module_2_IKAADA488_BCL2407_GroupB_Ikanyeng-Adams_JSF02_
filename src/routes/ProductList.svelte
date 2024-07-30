<script>
  import { onMount } from 'svelte';
  import { push } from 'svelte-spa-router';

  /**
   * @type {Array<Object>} products - List of all products fetched from the API
   */
  let products = [];

  /**
   * @type {Array<Object>} filteredProducts - List of products filtered based on selected category, search query, and sort option
   */
  let filteredProducts = [];

  /**
   * @type {boolean} loading - Indicates whether the products are still being loaded
   */
  let loading = true;

  /**
   * @type {Array<string>} categories - List of product categories
   */
  let categories = ["jewelery", "men's clothing", "women's clothing", "electronics"];

  /**
   * @type {string} selectedCategory - Currently selected category for filtering products
   */
  let selectedCategory = '';

  /**
   * @type {string} searchQuery - Current search query for filtering products by title
   */
  let searchQuery = '';

  /**
   * @type {string} sortOption - Current sort option for sorting products by price
   */
  let sortOption = 'default';

  /**
   * @type {boolean} noItemsFound - Indicates whether no products match the current filters
   */
  let noItemsFound = false;

  /**
   * Fetches products from the API and initializes the product list
   */
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

  /**
   * Navigates to the product detail page
   * @param {number} productId - ID of the product to view
   */
  const viewProduct = (productId) => {
    push(`/product/${productId}`);
  };

  /**
   * Filters and sorts the products based on selected category, search query, and sort option
   */
  const filterProducts = () => {
    filteredProducts = products
      .filter(product => 
        (!selectedCategory || product.category === selectedCategory) &&
        (!searchQuery || product.title.toLowerCase().includes(searchQuery.toLowerCase()))
      )
      .sort((a, b) => {
        if (sortOption === 'low') {
          return a.price - b.price;
        } else if (sortOption === 'high') {
          return b.price - a.price;
        } else {
          return 0;
        }
      });

    noItemsFound = filteredProducts.length === 0;
  };

  /**
   * Updates the product list based on the search query
   */
  const searchProducts = () => {
    filterProducts();
  };

  // Automatically filter products whenever the selected category, search query, or sort option changes
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
    margin-right: 100px;
    top: 0;
    right: 0;
    height: 100%;
    background-color: #3b82f6;
    color: white;
    border-left: 0;
    border-radius: 0 0.375rem 0.375rem 0;
  }

  #search-svg {
    size: 1px;
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
    width: 288px;
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

  .no-items-message {
    color: blue;
    text-align: center;
    margin-top: 2rem;
    font-size: 1.25rem;
  }

  @media (max-width: 768px) {
    .product-card {
      width: calc(50% - 2rem);
    }

    .search-button {
      margin-left: 20px;
    }
  }

  @media (max-width: 480px) {
    .product-card {
      width: calc(100% - 2rem);
    }

    .search-button {
      margin-left: 20px;
    }
  }
</style>

<main>
  <!-- Display loading message while products are being fetched -->
  {#if loading}
    <p>Loading...</p>
  {:else}
    <div class="container">
      <!-- Dropdown for selecting product category -->
      <div class="form-group">
        <select bind:value="{selectedCategory}" on:change="{filterProducts}" class="category-select">
          <option value="">All Categories</option>
          {#each categories as category}
            <option value="{category}">{category}</option>
          {/each}
        </select>

        <!-- Search input field for filtering products by title -->
        <div class="relative w-full">
          <input type="search" class="search-input" placeholder="Search products..." bind:value="{searchQuery}" on:input="{searchProducts}" />
          <button type="submit" class="search-button">
            <span class="sr-only">Search</span>
          </button>
        </div>
      </div>

      <!-- Dropdown for sorting products by price -->
      <div class="sort-group">
        <label for="sort" class="sort-label">Sort by</label>
        <select id="sort" bind:value="{sortOption}" on:change="{filterProducts}" class="sort-select">
          <option value="default">Default</option>
          <option value="low">Price: Low to High</option>
          <option value="high">Price: High to Low</option>
        </select>
      </div>
    </div>

    <!-- Display product cards or a message if no items are found -->
    <div class="products-container">
      {#if filteredProducts.length === 0}
        <p class="no-items-message">No items found</p>
      {:else}
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
      {/if}
    </div>
  {/if}
</main>

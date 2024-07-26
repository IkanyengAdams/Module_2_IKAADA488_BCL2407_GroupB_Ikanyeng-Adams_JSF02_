<script>
  import { onMount } from 'svelte';

  let categories = [ "Jewellery", "Men's Clothes", "Women's Clothes", "Electronics"];
  let selectedCategory = ''
  let searchQuery = '';
  let products = [];

  const filterProducts = () => {
  
  };

  const searchProducts = () => {
  
  };
</script>

<style>
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
</style>

<div class="container">
  <div class="form-group">
    <select
      bind:value="{selectedCategory}"
      on:change="{filterProducts}"
      class="category-select"
    >
      <option value="">All Categories</option>
      {#each categories as category}
        <option value="{category}">{category}</option>
      {/each}
    </select>
    
    <div class="relative w-full">
      <input
        type="search"
        class="search-input"
        placeholder="Search products..."
        bind:value="{searchQuery}"
        on:input="{searchProducts}"
      />
      <button type="submit" class="search-button">
        <svg
          class="w-4 h-4"
          aria-hidden="true"
          xmlns="http://www.w3.org/2000/svg"
          fill="none"
          viewBox="0 0 20 20"
        >
          <path
            stroke="currentColor"
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="m19 19-4-4m0-7A7 7 0 1 1 1 8a7 7 0 0 1 14 0Z"
          />
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

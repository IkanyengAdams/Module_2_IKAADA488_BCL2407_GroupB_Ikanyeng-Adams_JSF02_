<script>
  import { push } from 'svelte-spa-router';

  /**
   * @type {boolean} openSidebar - Indicates whether the sidebar is open or closed
   */
  let openSidebar = false;

   /**
   * Toggles the sidebar open or closed
   */

  function toggleSidebar() {
    openSidebar = !openSidebar;
  }

  /**
   * Navigates to the product list page
   */

  function goToProductList() {
    push('/');
  }

   /**
   * Navigates to the wishlist page
   */

  function goToWishlist() {
    push('/wishlist');
  }

  /**
   * Navigates to the cart page
   */

  function goToCart() {
    push('/cart');
  }

   /**
   * Navigates to the login page
   */

  function goToLogin() {
    push('/login');
  }
</script>

<style>
  .navbar {
    background-color: hsl(0, 9%, 69%);
    padding: 0.1px;
    height: 70px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    color: white;
    position: fixed;
    width: 100%;
    top: 0;
    left: 0;
    z-index: 1000;
  }

  .img {
    margin-left: 20px;
  }

  .heading {
    font-size: 30px;
    font-weight: bold;
    cursor: pointer;
  }

  .btn-toggle {
    cursor: pointer;
    padding: 20px;
    margin-right: 15px;
    background-color: hsl(0, 9%, 69%);
    color: wheat;
    border: none;
    font-size: 20px;
  }

  .sidebar {
    position: fixed;
    top: 0;
    left: 0;
    bottom: 0;
    width: 220px;
    background-color: hsl(0, 0%, 69%);
    box-shadow: 2px 0 5px rgba(0, 0, 0, 0.3);
    transform: translateX(-100%);
    transition: transform 0.8s ease-out;
    z-index: 999;
  }

  .sidebar.open {
    transform: translateX(0);
  }

  .navbar-items {
    display: flex;
    flex-direction: row;
    padding: 1rem;
    color: white;
  }

  .navbar-item {
    padding: 0.5rem;
    margin: 0.5rem 0;
    cursor: pointer;
  }

  .sidebar-items {
    display: flex;
    flex-direction: column;
    padding: 1rem;
    color: white;
  }

  .sidebar-item {
    padding: 0.5rem;
    margin: 0.5rem 0;
    cursor: pointer;
  }

  .menu-icon {
    display: none;
  }

  @media (max-width: 768px) {
    .menu-icon {
      display: block;
      margin-left: 2rem;
    }
    .navbar-items {
      display: none;
    }
    .sidebar {
      display: block;
    }
  }

  @media (min-width: 769px) {
    .sidebar {
      display: none;
    }
    .navbar-items {
      display: flex;
    }
  }
</style>

<main style="margin-top: 80px;">
  <header>
    <nav class="navbar">
      <div>
        <img class="img" src="public/android-chrome-192x192.png" alt="SwiftCart Logo" style="height: 32px;">
        <span class="heading" on:click={goToProductList}>SwiftCart</span>
      </div>
      <div class="navbar-items">
        <span class="navbar-item" on:click={goToWishlist}>Wishlist</span>
        <span class="navbar-item" on:click={goToCart}>Cart</span>
        <span class="navbar-item" on:click={goToLogin}>Login</span>
      </div>
      <button class="btn-toggle menu-icon" on:click={toggleSidebar}>
        &#9776;
      </button>
    </nav>
    <div class="sidebar {openSidebar ? 'open' : ''}">
      <div class="sidebar-items"><br>
        <br>
        <span class="sidebar-item" on:click={() => { toggleSidebar(); goToWishlist(); }}>Wishlist</span>
        <span class="sidebar-item" on:click={() => { toggleSidebar(); goToCart(); }}>Cart</span>
        <span class="sidebar-item" on:click={() => { toggleSidebar(); goToLogin(); }}>Login</span>
      </div>
    </div>
  </header>
</main>

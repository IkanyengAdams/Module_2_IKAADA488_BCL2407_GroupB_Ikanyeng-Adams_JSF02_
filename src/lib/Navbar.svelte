<script>
  let openSidebar = false;

  function toggleSidebar() {
    openSidebar = !openSidebar;
  }
</script>

<style>
  
</style>

<header>
  <nav class="navbar">
    <div>
      <img src="/online-shop.png" alt="SwiftCart Logo" style="height: 32px;">
      <span>SwiftCart</span>
    </div>
    <div class="nav-items">
      <span class="nav-item">Wishlist</span>
      <span class="nav-item">Cart</span>
      <a class="nav-item" href="/login.html">Login</a>
    </div>
    <button class="btn-toggle menu-icon" on:click={toggleSidebar}>
      &#9776;
    </button>
  </nav>
  <div class="sidebar {openSidebar ? 'open' : ''}">
    <div class="nav-items">
      <span class="nav-item" on:click={toggleSidebar}>Wishlist</span>
      <span class="nav-item" on:click={toggleSidebar}>Cart</span>
      <a class="nav-item" href="/login.html" on:click={toggleSidebar}>Login</a>
    </div>
  </div>
</header>


<main style="margin-top: 80px;">
  
</main>

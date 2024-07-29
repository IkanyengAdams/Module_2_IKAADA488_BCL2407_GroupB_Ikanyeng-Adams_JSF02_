<script>
  let openSidebar = false;

  function toggleSidebar() {
    openSidebar = !openSidebar;
  }
</script>

<style>
  .navbar {
    background-color: #4a4a4a;
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
  .btn-toggle {
    cursor: pointer;
    padding: 20px;
    margin-right: 15px;
    background-color: #4a4a4a;
    color: wheat;
    border: none;
    font-size: 20px;
  }
  .sidebar {
    position: fixed;
    top: 0;
    left: 0;
    bottom: 0;
    height: 200%;
    width: 220px;
    background-color: #4a4a4a;
    box-shadow: 2px 0 5px rgba(0, 0, 0, 0.1);
    transform: translateX(-100%);
    transition: transform 0.3s ease-out;
    z-index: 999;
  }
  .sidebar.open {
    transform: translateX(0);
  }
  .nav-items {
    display: flex;
    flex-direction: row;
    padding: 1rem;
    color: white;
  }
  .nav-item {
    padding: 0.5rem;
    margin: 0.5rem 0;
    cursor: pointer;
  }
  .nav-item:hover {
    background-color: #3a3a3a;
  }
  .menu-icon {
    display: none;

    
  }

  @media (max-width: 768px) {
    .menu-icon {
      display: block;
      margin-left: 2rem;
    }
    .nav-items {
      display: none;
    }
  }
</style>

<header>
  <nav class="navbar">
    <div>
      <img src="public/vite.svg" alt="SwiftCart Logo" style="height: 32px;">
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

<script>
  import { push } from 'svelte-spa-router';

  function mainPage() {
    push('/');
  }
</script>

<style>
  
  .go-back-button {
    margin-top: 20px;
    padding: 10px 20px;
    background-color: hsl(0, 9%, 69%);
    color: white;
    border: none;
    cursor: pointer;
  }
</style>

<main>
  <h1>Cart page</h1>
  <button class="go-back-button" on:click={mainPage}>Back</button>
</main>

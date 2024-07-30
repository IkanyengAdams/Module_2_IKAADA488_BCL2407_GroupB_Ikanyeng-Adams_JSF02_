<script>
  import { push } from 'svelte-spa-router';

  let email = '';
  let password = '';

  function handleLogin() {
    alert(`Logging in with email: ${email}`);
  }

  function mainPage() {
    push('/');
  }
</script>

<style>
 
</style>

<main>
  <div class="login-container">
    <h1>Login</h1>
    <div class="input-group">
      <input type="email" placeholder="Email" bind:value={email} />
    </div>
    <div class="input-group">
      <input type="password" placeholder="Password" bind:value={password} />
    </div>
    <button class="login-button" on:click={handleLogin}>Login</button>
    <button class="go-back-button" on:click={mainPage}>Back</button>
  </div>
</main>

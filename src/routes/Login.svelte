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
  body {
    font-family: 'Arial', sans-serif;
    background-color: #f3f4f6;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    margin: 0;
  }

  .login-container {
    background-color: white;
    padding: 2rem;
    border-radius: 10px;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
    width: 300px;
    text-align: center;
  }

  h1 {
    margin-bottom: 1.5rem;
    color: hsl(0, 9%, 30%);
  }

  .input-group {
    margin-bottom: 1rem;
  }

  .input-group input {
    width: 100%;
    padding: 0.75rem;
    border: 1px solid #ccc;
    border-radius: 5px;
    font-size: 1rem;
  }

  .login-button, .go-back-button {
    width: 100%;
    padding: 0.75rem;
    border: none;
    border-radius: 5px;
    font-size: 1rem;
    cursor: pointer;
  }

  .login-button {
    background-color: #3b82f6;
    color: white;
    margin-top: 1rem;
  }

  .login-button:hover {
    background-color: #2563eb;
  }

  .go-back-button {
    margin-top: 1rem;
    background-color: hsl(0, 9%, 69%);
    color: white;
  }

  .go-back-button:hover {
    background-color: hsl(0, 9%, 50%);
  }
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

<script>
  import { useNavigate } from 'svelte-navigator';
  const navigate = useNavigate();

  import { user } from './stores';
  let email = '';
  let password = '';
  let loading;
  let error = null;
  let loginResponse

  export let config;

  async function handleLogin() {
    // Perform login logic here
    // You can validate the username and password, make API calls, etc.
    const body = {
      email,
      password,
    }
    loading = true;
    try {
      const res = await fetch(`${config.app}:${config.appPort}/login`, {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify(body),
      });

      if (!res.ok) {
        // Handle the error response
        // const { error } = await res.json();
        throw new Error('The email or password is invalid');
      }

      let { token } = await res.json();
      user.set(token);
      navigate('/')
    } catch (err) {
      error = err.message;
      console.error(error);
    }

    loading = false;
  }

  function clearError() {
    // Clear the error message
    error = null;
  }

  function navigateToSignup() {
    navigate('/signup');
  }
</script>

<main>
  <h1>Login</h1>

  <form on:submit|preventDefault="{handleLogin}">
    <label for="email">Email:</label>
    <input type="text" id="email" bind:value="{email}" on:input="{clearError}"/>

    <label for="password">Password:</label>
    <input type="password" id="password" bind:value="{password}" on:input="{clearError}"/>

    <button disabled="{loading}" type="submit">Login</button>

    {#if error}
      <p class="error-text">{error}</p>
  {/if}
  </form>

  <p>If you don't have an account, <a href="/signup" on:click="{navigateToSignup}">please register</a>.</p>
</main>

<style>
  .error-text {
    color: red;
    font-size: 14px;
    margin-top: 5px;
  }

  main {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100vh;
    font-family: Arial, sans-serif;
    text-align: center;
  }

  h1 {
    font-size: 32px;
    margin-bottom: 30px;
    color: #333;
  }

  form {
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 300px;
    background-color: #fff;
    border-radius: 8px;
    padding: 30px;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  }

  label {
    font-size: 18px;
    margin-bottom: 10px;
    color: #555;
  }

  input {
    padding: 10px;
    margin-bottom: 15px;
    width: 100%;
    font-size: 16px;
    border: 1px solid #ccc;
    border-radius: 4px;
    transition: border-color 0.3s ease;
  }

  input:focus {
    outline: none;
    border-color: #007bff;
  }

  button {
    padding: 12px 24px;
    background-color: #007bff;
    color: #fff;
    border: none;
    border-radius: 4px;
    font-size: 16px;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }

  button:hover {
    background-color: #0056b3;
  }
</style>
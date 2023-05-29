<script>
  import { useNavigate } from 'svelte-navigator';
  import { onMount } from 'svelte';

  const navigate = useNavigate();
  let email, firstName, lastName, role, password, confirmPassword;
  let passwordError = '';

  function handleSignup() {
    if (password !== confirmPassword) {
      passwordError = 'Passwords must match';
      return;
    }

    // Perform signup logic here
    // You can validate the username and password, make API calls, etc.
    console.log('Signing up...');
    console.log('Username:', username);
    console.log('Password:', password);
  }

  function navigateToLogin() {
    navigate('/login');
  }

  // Clear the password error message on component mount
  onMount(() => {
    passwordError = '';
  });

  // Function to handle password input
  function handlePasswordInput() {
    if (password === confirmPassword) {
      passwordError = '';
    }
  }
</script>

<main>
  <h1>Signup</h1>

  <form on:submit|preventDefault="{handleSignup}">
    <label for="firstName">First Name:</label>
    <input type="text" id="firstName" bind:value="{firstName}" />

    <label for="lastName">Last Name:</label>
    <input type="text" id="lastName" bind:value="{lastName}" />

    <label for="role">Role:</label>
    <select id="role" bind:value="{role}">
      <option value="">Select Role</option>
      <option value="Patient">Patient</option>
      <option value="Parent of Patient">Parent of Patient</option>
      <option value="Clinician">Clinician</option>
    </select>

    <label for="email">Email:</label>
    <input type="text" id="email" bind:value="{email}" />

    <label for="password">Password:</label>
    <input type="password" id="password" bind:value="{password}" />

    <label for="confirmPassword">Confirm Password:</label>
    <input type="password" id="confirmPassword" bind:value="{confirmPassword}" on:input="{handlePasswordInput}" class:error="{password !== confirmPassword}" />
    {#if password !== confirmPassword}
      <small class="error-text">Passwords must match</small>
    {/if}

    <button type="submit">Signup</button>
  </form>

  <p>If you already have an account, <a href="/login" on:click="{navigateToLogin}">please login</a>.</p>
</main>

<style>
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
    align-items: flex-start; /* Update to align labels to the left */
    width: 600px; /* Update the width to 600px or any desired value */
    background-color: #fff;
    border-radius: 8px;
    padding: 30px;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  }

  label {
    font-size: 18px;
    margin-bottom: 10px;
    color: #555;
    text-align: left; /* Align the labels to the left */
  }

  input,
  select {
    padding: 10px;
    margin-bottom: 15px;
    width: 100%;
    font-size: 16px;
    border: 1px solid #ccc;
    border-radius: 4px;
    transition: border-color 0.3s ease;
  }

  input:focus,
  select:focus {
    outline: none;
    border-color: #007bff;
  }

  input.error {
    border-color: red;
  }

  input.error {
    border-color: red;
  }

  .error-text {
    color: red;
    font-size: 14px;
    margin-top: 5px;
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
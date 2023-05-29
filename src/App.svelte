<script>
  import { Router, Route } from 'svelte-navigator';
  import Login from './Login.svelte';
  import Signup from './Signup.svelte';
  import Home from './Home.svelte';

  const config = {
	  "app": __myapp["env"].APP_HOST,
	  "appPort":__myapp["env"].APP_PORT
	}
</script>

<main>
  <Router>
      <Route path="signup">
        <Signup />
      </Route>
      <Route path="login">
        <Login config={config}/>
      </Route>
      <Route path="/">
        <Home />
      </Route>
  </Router>
</main>

<style>
  main {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
  }
</style>
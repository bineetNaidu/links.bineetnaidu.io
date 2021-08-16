<script>
  import Profile from './Profile.svelte';
  import Links from './Links.svelte';
</script>

<main class="container">
  <Profile />
  <Links />
</main>

<style scoped>
  .container {
    width: 100%;
    height: 100%;
    display: flex;
    margin: 2rem auto;
    justify-content: center;
    display: flex;
    flex-direction: column;
  }
</style>

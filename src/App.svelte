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
    width: 65%;
    height: 100%;
    display: flex;
    margin: auto;
    padding: 2rem 0;
    justify-content: center;
    display: flex;
    flex-direction: column;
  }

  @media (max-width: 550px) {
    .container {
      width: 95%;
    }
  }
</style>

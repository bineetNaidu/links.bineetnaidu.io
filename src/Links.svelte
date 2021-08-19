<script>
  import { onMount } from 'svelte';
  import axios from 'axios';

  let links = [];
  let loading = true;

  onMount(async () => {
    const { data } = await axios.get(process.env.API_URL);
    if (data.success) {
      links = data.data;
      loading = false;
    }
  });
</script>

<section>
  <ul class="links">
    {#if loading}
      {#each [1, 2, 3, 4, 5] as i (i)}
        <li>
          <div class="loader"><i class="fas fa-atom" /></div>
        </li>
      {/each}
    {:else}
      {#each links as l (l._id)}
        <li class="link">
          <a href={l.url}>
            <i class={l.icon} />
          </a>
          <span class="label">{l.label}</span>
        </li>
      {/each}
    {/if}
  </ul>
</section>

<style scoped>
  section {
    width: 70%;
    margin: auto;
    padding-top: 2rem;
    color: rgb(57, 224, 155);
  }

  .link i {
    color: rgb(57, 224, 155);
  }

  .links {
    display: flex;
    justify-content: center;
    list-style: none;
    padding: 0;
    margin: 0;
    flex-wrap: wrap;
    width: 100%;
  }

  .loader > i {
    font-size: 2rem;
    margin: 0 1.5rem;
    transition: all 0.3s ease-in-out;
    animation: spin-n-scale 2s infinite ease-in-out;
  }

  .link {
    height: 80px;
    width: 80px;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: all 100ms cubic-bezier(0.23, 1, 0.32, 1) 0s;
    z-index: 0;
    padding: 5px;
    border-radius: 9px;
    position: relative;
  }

  .link:hover {
    background-color: rgba(57, 224, 154, 0.289);
    box-shadow: 0 0 0 1px rgba(57, 224, 154, 0.289);
  }

  .link:hover i {
    transform: scale(1.1);
  }

  .label {
    position: absolute;
    bottom: -25px;
    font-weight: 500;
    transform: scale(0);
    transition: all 300ms cubic-bezier(0.23, 1, 0.32, 1) 0s;
  }

  .link:hover .label {
    transform: scale(1);
    transform-origin: top;
  }

  .link a {
    text-decoration: none;
    font-size: 2rem;
  }

  @keyframes spin-n-scale {
    0% {
      -webkit-transform: scale(0.5) rotate(0deg);
      transform: scale(0.5) rotate(0deg);
    }
    50% {
      -webkit-transform: scale(1.1) rotate(360deg);
      transform: scale(1.1) rotate(360deg);
    }
    100% {
      -webkit-transform: scale(0.5) rotate(720deg);
      transform: scale(0.5) rotate(720deg);
    }
  }
</style>

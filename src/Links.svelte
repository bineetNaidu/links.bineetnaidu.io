<script>
  import { onMount } from 'svelte';
  import axios from 'axios';

  let links = [];

  onMount(async () => {
    const { data } = await axios.get(
      'http://api-bineetnaidu-io.herokuapp.com/api/links'
    );
    if (data.success) {
      links = data.data;
    }
  });
</script>

<section>
  <ul class="links">
    {#each links as l (l._id)}
      <li class="link">
        <a href={l.url}>
          <i class={l.icon} />
        </a>
        <span class="label">{l.label}</span>
      </li>
    {/each}
  </ul>
</section>

<style scoped>
  section {
    display: flex;
    justify-content: center;
    width: 70%;
    margin: auto;
    padding-top: 2rem;
    color: rgb(57, 224, 155);
  }

  .link i {
    color: rgb(57, 224, 155);
  }

  .links {
    display: grid;
    list-style: none;
    padding: 0;
    margin: 0;
    grid-template-columns: repeat(5, 1fr);
    gap: 5px;
    width: 100%;
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
</style>

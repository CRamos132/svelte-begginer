<script lang="ts">
  import Inner from "./Inner.svelte";

  function handleMessage(event) {
    alert(event.detail.text);
  }
  export let name: string;
  let count: number = 0;
  let newItem = "";
  let list = [];
  $: doubled = count * 2;
  $: divisible = count % 3 === 0;
  const handleClick = () => {
    count++;
  };
  const handleItem = () => {
    list = [...list, newItem];
    newItem = "";
  };
</script>

<main>
  <h1>Hello {name}!</h1>
  <Inner on:message={handleMessage} />
  <p>{count} doubled is {doubled}</p>
  <button on:click={handleClick}>Clicked {count} times</button>
  {#if divisible && count !== 0}
    <p>{count} is divisible by 3</p>
  {:else}
    <p>{count} is not divisible by 3</p>
  {/if}
  <p>Add item: {newItem}</p>
  <input type="text" bind:value={newItem} placeholder="New item" />
  <button on:click={handleItem}>Add to list</button>
  <ul>
    {#each list as animal, i}
      <li>{i + 1} - {animal}</li>
    {/each}
  </ul>
</main>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  ul {
    list-style: none;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>

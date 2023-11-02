<script>
  export let type = "primary";
  export let flat = false;
  export let inverse = false;
</script>

<!-- svelte-ignore missing-declaration -->
<button class={type} class:flat class:inverse on:click>
  <slot />
</button>

<style>
  button {
    border: 0;
    cursor: pointer;
    border-radius: 6px;
    padding: 8px 12px;
    font-weight: bold;
    box-shadow: 3px 4px 5px rgba(0, 0, 0, 0.2);
    transition: 0.2s;
  }
  button:hover {
    font-size: 15px;
  }
  .primary {
    background: #d91b42;
    color: white;
  }
  .secondary {
    background: #45c496;
    color: white;
  }
  .flat {
    box-shadow: none;
  }
  .primary.inverse {
    color: #d91b42;
    background: white;
    border: 2px solid #d91b42;
  }
  .secondary.inverse {
    color: #45c496;
    background: white;
    border: 2px solid #45c496;
  }
</style>

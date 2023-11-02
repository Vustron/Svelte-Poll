<script>
  // import { onMount, onDestroy } from "svelte";
  import { fade, scale } from "svelte/transition";
  import { flip } from "svelte/animate";
  import PollStore from "../Store/PollStore";
  import PollDetails from "./PollDetails.svelte";

  // export let polls = [];

  // const unsub = PollStore.subscribe((data) => {
  //   polls = data;
  // });

  // // Maybe get data from a db
  // // @ts-ignore
  // onMount(() => {
  //   console.log("component mounted");
  // });

  // // Unsubscribe from the store
  // // @ts-ignore
  // onDestroy(() => {
  //   console.log("component destroyed");
  //   unsub();
  // });
</script>

<div class="poll-list" in:fade>
  {#each $PollStore as poll (poll.id)}
    <div out:scale|local animate:flip={{ duration: 500 }}>
      <PollDetails {poll} />
    </div>
  {/each}
</div>

<style>
  .poll-list {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 20px;
  }
</style>

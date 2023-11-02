<script>
  // @ts-nocheck

  import CreatePollForm from "./lib/Components/CreatePollForm.svelte";
  import Footer from "./lib/Components/Footer.svelte";
  import Header from "./lib/Components/Header.svelte";
  import PollList from "./lib/Components/PollList.svelte";
  import Tabs from "./lib/Shared/Tabs.svelte";

  // Tabs
  let items = ["Current Polls", "Add New Poll"];
  let activeItem = "Current Polls";
  const tabChange = (e) => {
    activeItem = e.detail;
  };

  // Handle Add New Polls
  const handleAdd = (e) => {
    activeItem = "Current Polls";
  };
</script>

<Header />

<main>
  <Tabs {activeItem} {items} on:tabChange={tabChange} />
  {#if activeItem === "Current Polls"}
    <PollList />
  {:else if activeItem === "Add New Poll"}
    <CreatePollForm on:add={handleAdd} />
  {/if}
</main>

<Footer />

<style>
  main {
    max-width: 960px;
    margin: 40px auto;
  }
</style>

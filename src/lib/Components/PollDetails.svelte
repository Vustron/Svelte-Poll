<script>
  import { tweened } from "svelte/motion";
  import PollStore from "../Store/PollStore";
  import Card from "../Shared/Card.svelte";
  import Button from "../Shared/Button.svelte";

  export let poll;

  // Reactive Values
  $: totalVotes = poll.votesA + poll.votesB;
  $: percentA = Math.floor((100 / totalVotes) * poll.votesA) || 0;
  $: percentB = Math.floor((100 / totalVotes) * poll.votesB) || 0;

  //   Tweened percentages
  const tweenedA = tweened(0);
  const tweenedB = tweened(0);
  $: tweenedA.set(percentA);
  $: tweenedB.set(percentB);
  //   $: console.log($tweenedA, $tweenedB);

  //  Handle Votes
  const handleVote = (option, id) => {
    PollStore.update((currentPolls) => {
      let copiedPolls = [...currentPolls];
      let upvotedPoll = copiedPolls.find((poll) => poll.id == id);

      if (option === "a") {
        upvotedPoll.votesA++;
      }
      if (option === "b") {
        upvotedPoll.votesB++;
      }

      return copiedPolls;
    });
  };

  //   Handle Delete
  const handleDelete = (id) => {
    PollStore.update((currentPolls) => {
      return currentPolls.filter((poll) => poll.id != id);
    });
  };
</script>

<Card>
  <div>
    <h3>{poll.question}</h3>
    <p>Totals Votes: {totalVotes}</p>
    <!-- svelte-ignore a11y-click-events-have-key-events -->
    <!-- svelte-ignore a11y-no-static-element-interactions -->
    <div class="answer" on:click={() => handleVote("a", poll.id)}>
      <div class="percent percent-a" style="width: {$tweenedA}%">
        <span>{poll.answerA}({poll.votesA})</span>
      </div>
    </div>
    <!-- svelte-ignore a11y-click-events-have-key-events -->
    <!-- svelte-ignore a11y-no-static-element-interactions -->
    <div class="answer" on:click={() => handleVote("b", poll.id)}>
      <div class="percent percent-b" style="width: {$tweenedB}%">
        <span>{poll.answerB}({poll.votesB})</span>
      </div>
    </div>
    <div class="delete">
      <Button on:click={() => handleDelete(poll.id)}>Delete</Button>
    </div>
  </div>
</Card>

<style>
  h3 {
    margin: 0;
    color: #555;
  }
  p {
    margin-top: 6px;
    font-size: 14px;
    color: #aaa;
    margin-bottom: 30px;
  }
  .answer {
    background: #fafafa;
    cursor: pointer;
    margin: 10px auto;
    position: relative;
  }
  .answer:hover {
    opacity: 0.6;
  }
  span {
    display: inline-block;
    padding: 10px 20px;
  }
  .percent {
    height: 100%;
    position: relative;
    box-sizing: border-box;
  }
  .percent-a {
    border-left: 4px solid #d91b42;
    background: rgba(217, 27, 66, 0.4);
  }
  .percent-b {
    border-left: 4px solid #45c496;
    background: rgba(69, 180, 150, 0.4);
  }
  .delete {
    margin-top: 30px;
    text-align: center;
  }
</style>

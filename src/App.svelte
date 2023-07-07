<script>
  import Team from "./lib/Team.svelte";
  let blueScore = 20;
  let redScore = 20;
  $: blueWon = redScore === 0;
  $: redWon = blueScore === 0;
  $: gameOver = blueWon || redWon;
  function resetGame() {
    blueScore = 20;
    redScore = 20;
  }
</script>

<div class="row mt-2">
  <div class="col">
    <h1 class="text-center">MTG COUNTER</h1>
  </div>
</div>

<div class="row">
  <div class="col">
    <Team {gameOver} bind:score={redScore} team="Red" />
  </div>
  <div class="col">
    <Team {gameOver} team="Blue" bind:score={blueScore} />
  </div>
</div>
{#if gameOver}
  <div class="row">
    <div class="col text-center">
      {#if blueWon}
        <h2 style="color:blue">Blue Won</h2>
      {:else}
        <h2 style="color:red">Red won</h2>
      {/if}
    </div>
  </div>
  <div class="row mt-2">
    <div class="col">
      <button on:click={resetGame} class="btn btn-warning w-100"
        >Reset Game</button
      >
    </div>
  </div>
{:else}
  <div class="row mt-2">
    <div class="col">
      <button on:click={resetGame} class="btn btn-success w-100"
        >New Game</button
      >
    </div>
  </div>
{/if}

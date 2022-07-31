<script>
  import Player from "./lib/Player.svelte";
  let player1Score = 0;
  let player2Score = 0;

  function reset() {
    player1Score = 0;
    player2Score = 0;
  }
</script>

<main>
  <Player bind:score={player1Score} playerName="Player 1" />
  <Player bind:score={player2Score} playerName="Player 2" />
  <button on:click={reset} class="contrast outline">RESET</button>
</main>

<style>
</style>

<script>
  export let playerName;

  export let score = 0;
  function increment() {
    score++;
  }

  function decrement() {
    score--;

    if (score < 0) {
      score = 0;
    }
  }
</script>

<div>
  <h2 class="center">{playerName}</h2>
  <h3 class="center">{score}</h3>
  <button on:click={increment}>Increase</button>
  <button on:click={decrement}>Decrease</button>
</div>

<style>
  .center {
    text-align: center;
  }
</style>

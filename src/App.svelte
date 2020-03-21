<script>
  import Board from './Board.svelte'
	let numAnts = 5
</script>

<style>
	h1 input {
		width: 3em;
	}
</style>

<header>
  <h1>
    Ants
		<input type="number" bind:value={numAnts}>
  </h1>
</header>

<main>
  <Board size={{x: 800, y: 600}} {numAnts}/>
</main>

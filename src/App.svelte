<script>
  import Board from './Board.svelte'
	let numAnts = 5
  let showInfo = false
</script>

<style>
	h1 input[type=number] {
		width: 3em;
	}

  h1 label {
    display: inline-block;
    padding-left: 1em;
  }
</style>

<header>
  <h1>
    Ants
		<input type="number" bind:value={numAnts}>
    <label>
		  <input type="checkbox" bind:checked={showInfo}>
      Info
    </label>
  </h1>
</header>

<main>
  <Board size={{x: 800, y: 600}} {numAnts} {showInfo}/>
</main>

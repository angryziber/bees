<script>
  import Ant from './Ant.svelte'
  export let numAnts, showInfo
  let board, boardSize
  $: if (board) {
    const rect = board.getBoundingClientRect()
    boardSize = {x: rect.width, y: rect.height}
  }
</script>

<style>
  .board {
    background: white;
    border: 1px solid grey;
    margin: auto;
    position: relative;
    width: 80vw;
    height: 80vh;
  }
</style>

<div bind:this={board} class="board">
  {#if boardSize}
    {#each Array(numAnts) as a, i}
      <Ant {showInfo} {boardSize}/>
    {/each}
  {/if}
</div>

<script>
  import {setContext} from 'svelte'
  import Bee from './Bee.svelte'
  export let numBees, showInfo
  setContext('bees', [])
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
    {#each Array(numBees) as a, i}
      <Bee {i} {showInfo} {boardSize}/>
    {/each}
  {/if}
</div>

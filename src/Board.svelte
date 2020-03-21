<script>
  import Ant from './Ant.svelte'
  export let size
  export let numAnts
</script>

<style>
  .board {
    background: white;
    border: 1px solid grey;
    margin: auto;
    position: relative;
  }
</style>

<div class="board" style="width: {size.x}px; height: {size.y}px">
  {#each Array(numAnts) as a, i}
    <Ant boardSize={size}/>
  {/each}
</div>

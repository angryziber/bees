<script>
  import config from './config'
  import Ant from './Ant.svelte'
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

<div class="board" style="width: {config.boardSize.x}px; height: {config.boardSize.y}px; padding-right: {config.antSize}px; padding-bottom: {config.antSize}px">
  {#each Array(numAnts) as a, i}
    <Ant/>
  {/each}
</div>

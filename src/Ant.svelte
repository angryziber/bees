<script>
  import {onDestroy, onMount} from 'svelte'
  import config from './config'

  const size = 16
  const halfSize = size / 2
  const color = '#' + Math.floor(Math.random() * 0xDDDDDD).toString(16).padStart(6, '0')
  const antCss = `width: ${size}px; height: ${size}px; background-color: ${color}`
  let x = Math.random() * config.boardSize.x
  let y = Math.random() * config.boardSize.y
  let speed = Math.random() * 5

  function step() {
    x += speed
    respectBoundaries()
  }

  function respectBoundaries() {
    if (x < 0) x = 0
    else if (x > config.boardSize.x) x = config.boardSize.x
    if (y < 0) y = 0
    else if (y > config.boardSize.y) y = config.boardSize.y
  }

  let interval
  onMount(() => interval = setInterval(step, 60))
  onDestroy(() => clearInterval(interval))
</script>

<style>
  .ant {
    border-radius: 50%;
    background: grey;
    position: absolute;
  }
</style>

<div class="ant-wrapper" style="transform: translate({x}px, {y}px)">
  <div class="ant" style="{antCss}"></div>
</div>
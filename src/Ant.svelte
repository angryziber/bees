<script>
  import {onDestroy, onMount} from 'svelte'
  import config from './config'

  export let showInfo

  const size = 16
  const halfSize = size / 2
  const color = '#' + Math.floor(Math.random() * 0xDDDDDD).toString(16).padStart(6, '0')
  const antCss = `width: ${size}px; height: ${size}px; background-color: ${color}`
  let x = Math.random() * config.boardSize.x
  let y = Math.random() * config.boardSize.y
  let speedx = Math.random() * 5
  let speedy = Math.random() * 5

  function step() {
    x += speedx
    y += speedy
    respectBoundaries()
  }

  function respectBoundaries() {
    if (x <= 0) speedx = -speedx
    else if (x >= config.boardSize.x) speedx = -speedx

    if (y <= 0) speedy = -speedy
    else if (y >= config.boardSize.y) speedy = -speedy
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

  .info {
    position: absolute;
    top: 20px;
    background: rgba(255,255,255,0.7)
  }
</style>

<div class="ant-wrapper" style="transform: translate({x}px, {y}px)">
  <div class="ant" style="{antCss}"></div>
  {#if showInfo}
    <div class="info">{Math.round(x)} {Math.round(y)}; speed: {Math.round(speedx)} {Math.round(speedy)}</div>
  {/if}
</div>
<script>
  import {onDestroy, onMount} from 'svelte'
  import config from './config'

  export let showInfo

  let size = 16
  const halfSize = size / 2
  const color = '#' + Math.floor(Math.random() * 0xDDDDDD).toString(16).padStart(6, '0')
  let x = Math.random() * config.boardSize.x
  let y = Math.random() * config.boardSize.y
  let speedx = Math.random() * 5
  let speedy = Math.random() * 5

  let numSteps = 0

  function step() {
    respectBoundaries()
    x += speedx
    y += speedy
    if (++numSteps >= 10) {
      numSteps = 0
      speedx += Math.random() * 3
      speedy += Math.random() * 3
    }
  }

  function respectBoundaries() {
    if (x <= 0) {
      reverseX()
      x = 0
    }
    else if (x >= config.boardSize.x - size) {
      reverseX()
      x = config.boardSize.x - size
    }
    if (y <= 0) {
      reverseY()
      y = 0
    }
    else if (y >= config.boardSize.y - size) {
      reverseY()
      y = config.boardSize.y - size
    }
  }

  function reverseX() {
    speedx = -speedx
    size = size - Math.random() * 5
  }

  function reverseY() {
    speedy = -speedy
    size = size + Math.random() * 5
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
    color: white;
    text-align: center;
  }

  .info {
    position: absolute;
    top: 20px;
    background: rgba(255,255,255,0.7)
  }
</style>

<div class="ant-wrapper" style="transform: translate({x}px, {y}px)">
  <div class="ant" style="width: {size}px; height: {size}px; background-color: {color}; font-size: {size}px">&#128028;</div>
  {#if showInfo}
    <div class="info">{Math.round(x)} {Math.round(y)}; speed: {Math.round(speedx)} {Math.round(speedy)}</div>
  {/if}
</div>
<script>
  import {onDestroy, onMount} from 'svelte'

  export let showInfo, boardSize

  const color = '#' + Math.floor(Math.random() * 0xDDDDDD).toString(16).padStart(6, '0')

  let size = 24
  let x = Math.random() * boardSize.x
  let y = Math.random() * boardSize.y
  let speedx = rnd(5)
  let speedy = rnd(5)

  let numSteps = 0

  function step() {
    x += speedx
    y += speedy
    if (++numSteps >= 10) {
      numSteps = 0
      speedx += rnd(3)
      speedy += rnd(3)
    }
    checkBoundaries()
  }

  function checkBoundaries() {
    if (x <= 0) {
      reverseX()
      x = 0
    }
    else if (x >= boardSize.x - size) {
      reverseX()
      x = boardSize.x - size
    }
    if (y <= 0) {
      reverseY()
      y = 0
    }
    else if (y >= boardSize.y - size) {
      reverseY()
      y = boardSize.y - size
    }
  }

  function reverseX() {
    speedx = -speedx
    size -= Math.random() * 5
  }

  function reverseY() {
    speedy = -speedy
    size += Math.random() * 5
  }

  function rnd(max) {
    return (Math.random() - 0.5) * max
  }

  let interval
  onMount(() => interval = setInterval(step, 16))
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

  .icon {
    display: block;
    transform: translate(-0.1em, -0.1em);
  }

  .info {
    position: absolute;
    top: 20px;
    background: rgba(255,255,255,0.7)
  }
</style>

<div class="ant-wrapper" style="transform: translate({x}px, {y}px)">
  <div class="ant" style="width: {size}px; height: {size}px; background-color: {color}; font-size: {size}px">
    <span class="icon">&#x1F41D;</span>
  </div>
  {#if showInfo}
    <div class="info">{Math.round(x)} {Math.round(y)}; speed: {Math.round(speedx)} {Math.round(speedy)}</div>
  {/if}
</div>
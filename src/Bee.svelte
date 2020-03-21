<script>
  import {onDestroy, onMount} from 'svelte'

  export let showInfo, boardSize

  export let bee = {
    size: 24,
    color: '#' + Math.floor(Math.random() * 0xDDDDDD).toString(16).padStart(6, '0'),
    x: Math.random() * boardSize.x,
    y: Math.random() * boardSize.y,
    speedx: rnd(5),
    speedy: rnd(5)
  }

  let numSteps = 0

  function step() {
    bee.x += bee.speedx
    bee.y += bee.speedy
    if (++numSteps >= 10) {
      numSteps = 0
      bee.speedx += rnd(3)
      bee.speedy += rnd(3)
    }
    checkBoundaries()
  }

  function checkBoundaries() {
    if (bee.x <= 0) {
      reverseX()
      bee.x = 0
    }
    else if (bee.x >= boardSize.x - bee.size) {
      reverseX()
      bee.x = boardSize.x - bee.size
    }
    if (bee.y <= 0) {
      reverseY()
      bee.y = 0
    }
    else if (bee.y >= boardSize.y - bee.size) {
      reverseY()
      bee.y = boardSize.y - bee.size
    }
  }

  function reverseX() {
    bee.speedx = -bee.speedx
    bee.size -= Math.random() * 5
  }

  function reverseY() {
    bee.speedy = -bee.speedy
    bee.size += Math.random() * 5
  }

  function rnd(max) {
    return (Math.random() - 0.5) * max
  }

  let interval
  onMount(() => interval = setInterval(step, 16))
  onDestroy(() => clearInterval(interval))
</script>

<style>
  .bee {
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
    top: 30px;
    background: rgba(255,255,255,0.7)
  }
</style>

<div style="transform: translate({bee.x}px, {bee.y}px)">
  <div class="bee" style="width: {bee.size}px; height: {bee.size}px; background-color: {bee.color}; font-size: {bee.size}px">
    <span class="icon">&#x1F41D;</span>
  </div>
  {#if showInfo}
    <div class="info">{Math.round(bee.x)} {Math.round(bee.y)}; speed: {Math.round(bee.speedx)} {Math.round(bee.speedy)}</div>
  {/if}
</div>
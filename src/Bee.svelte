<script>
  import {onDestroy, onMount, getContext} from 'svelte'

  export let i, showInfo, boardSize

  const defaultSize = 24
  const bee = {
    size: defaultSize,
    color: '#' + Math.floor(Math.random() * 0xDDDDDD).toString(16).padStart(6, '0'),
    x: Math.random() * (boardSize.x - defaultSize) + defaultSize / 2,
    y: Math.random() * (boardSize.y - defaultSize) + defaultSize / 2,
    speedx: rnd(5),
    speedy: rnd(5)
  }

  const allBees = getContext('bees')
  allBees[i] = bee

  let numSteps = 0

  function step() {
    bee.x += bee.speedx
    bee.y += bee.speedy
    if (++numSteps >= 10) {
      numSteps = 0
      bee.speedx += rnd(3)
      bee.speedy += rnd(3)
    }
    checkCollisions()
    checkBoundaries()
  }

  function checkCollisions() {
    allBees.forEach(b => {
      if (b === bee) return
      const xd = Math.abs(b.x - bee.x)
      const yd = Math.abs(b.y - bee.y)
      const distance = Math.sqrt(Math.pow(xd, 2) + Math.pow(yd, 2))
      if (distance <= b.size + bee.size) {
        if (xd > yd) bee.speedx = -bee.speedx
        else bee.speedy = -bee.speedy
      }
    })
  }

  function checkBoundaries() {
    const halfSize = bee.size / 2
    if (bee.x <= halfSize) {
      reverseX()
      bee.x = halfSize
    }
    else if (bee.x >= boardSize.x - halfSize) {
      reverseX()
      bee.x = boardSize.x - halfSize
    }
    if (bee.y <= halfSize) {
      reverseY()
      bee.y = halfSize
    }
    else if (bee.y >= boardSize.y - halfSize) {
      reverseY()
      bee.y = boardSize.y - halfSize
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
  <div class="bee" style="width: {bee.size}px; height: {bee.size}px; background-color: {bee.color}; font-size: {bee.size}px; transform: translate({-bee.size/2}px, {-bee.size/2}px)">
    <span class="icon">&#x1F41D;</span>
  </div>
  {#if showInfo}
    <div class="info">{Math.round(bee.x)} {Math.round(bee.y)}; speed: {Math.round(bee.speedx)} {Math.round(bee.speedy)}</div>
  {/if}
</div>

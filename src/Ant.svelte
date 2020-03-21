<script>
  export let boardSize
  const size = 16
  const color = '#' + Math.floor(Math.random() * 0xDDDDDD).toString(16).padStart(6, '0')
  const css = `width: ${size}px; height: ${size}px; background-color: ${color}`
  let x = Math.random() * (boardSize.x - size) + size / 2
  let y = Math.random() * (boardSize.y - size) + size / 2
</script>

<style>
  .ant {
    border-radius: 50%;
    background: grey;
    position: absolute;
  }
</style>

<div class="ant" style="left: {x}px; top: {y}px; {css}">
</div>
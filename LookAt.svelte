<script>
  let x = 0
  let y = 0
  let style = ''
  let container = null
  export let intensity = 1
  function perspective({ clientX, clientY }) {
    let box = container.getBoundingClientRect()
    x = (-(clientY - box.y - box.height / 2) / 2000) * intensity
    y = ((clientX - box.x - box.width / 2) / 2000) * intensity
  }

  window.addEventListener(
    'deviceorientation',
    ({ beta, gamma }) => {
      if (beta && gamma) {
        x = ((-beta + 80) / 40) * intensity
        y = (-gamma / 40) * intensity
      }
    },
    true
  )
  function reset() {
    x = 0
    y = 0
  }

  $: window.requestAnimationFrame(() => (style = `--transform: perspective(100px) rotateX(${x}deg) rotateY(${y}deg)`))
</script>

<div {...$$restProps} on:mousemove={perspective} on:mouseleave={reset} bind:this={container} {style}>
  <slot />
</div>

<style>
  div > :global(*) {
    transform: var(--transform) !important;
    transition: transform ease 0.2s;
  }
</style>

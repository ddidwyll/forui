<div
  id="fr-slider{index}"
  on:mousedown={e => mousedown(e, index)}
  on:mouseup={() => reset()}
  on:mouseleave={() => reset()}
  on:mousemove={e => scroll(e, index)}>
  <slot />
</div>

<script>
  export let index = 1
  let slider = document.getElementById('fr-slider' + index)
  let startX = null
  let scrollLeft = null

  const reset = () => {
    if (!slider) return
    slider.classList.remove('scroll')
    startX = null
    scrollLeft = null
  }
  const mousedown = (e, index) => {
    console.log(slider)
    startX = e.pageX - slider.offsetLeft
    scrollLeft = slider.scrollLeft
  }
  const scroll = (e, index) => {
    if (!slider || slider.id !== 'fr-lider' + index) return
    if (slider.scrollWidth <= slider.clientWidth) return
    e.preventDefault()
    slider.classList.add('scroll')
    const walk = e.pageX - slider.offsetLeft - startX
    slider.scrollLeft = scrollLeft - walk
  }
</script>

<style>
  div {
    overflow: auto;
  }
  :global(.scroll) {
    cursor: ew-resize;
  }
  :global(.scroll > *) {
    pointer-events: none;
  }
  div::-webkit-scrollbar {
    display: none;
  }
</style>

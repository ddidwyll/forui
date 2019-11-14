{#if window.orientation}
  <div>
    <slot />
  </div>
{:else}
  <div
    bind:this={slider}
    class:scroll={$isScroll}
    on:mousedown={e => click(e)}
    on:mouseup={() => reset()}
    on:mouseleave={() => reset()}
    on:mousemove={e => scroll(e)}>
    <slot />
  </div>
{/if}

<script>
  import { onMount } from 'svelte'
  import { writable } from 'svelte/store'

  let ready = false
  const isScroll = writable(false)
  let slider
  let startX = null
  let scrollLeft = null
  let reset = () => {}
  let click = () => {}
  let scroll = () => {}

  onMount(() => {
    if (window.orientation) return
    reset = () => {
      isScroll.set(false)
      startX = null
      scrollLeft = null
      ready = false
    }
    click = (e, index) => {
      if (slider.scrollWidth <= slider.clientWidth) return
      ready = true
      startX = e.pageX - slider.offsetLeft
      scrollLeft = slider.scrollLeft
    }
    scroll = (e, index) => {
      if (!ready) return
      isScroll.set(true)
      e.preventDefault()
      const walk = e.pageX - slider.offsetLeft - startX
      slider.scrollLeft = scrollLeft - walk
    }
  })
</script>

<style>
  div {
    overflow-x: auto;
    overflow-y: hidden;
  }
  div > :global(*) {
    min-width: intrinsic !important;
    min-width: max-content !important;
  }
  div.scroll {
    cursor: ew-resize;
  }
  div.scroll > :global(*) {
    pointer-events: none;
  }
  div::-webkit-scrollbar {
    display: none;
  }
</style>

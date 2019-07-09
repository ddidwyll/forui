<div class:scrollx class:scrolly>
  <slot />
</div>

<script>
  export let scrollx = false
  export let scrolly = false
</script>

<style>
  div {
    width: var(--container-width);
    max-width: var(--container-max-width);
    box-sizing: border-box;
    height: 100%;
    max-height: 100%;
    background-color: var(--white-bg);
    overflow: hidden;
    margin: 0 auto;
  }
  div.scrollx {
    overflow-x: auto;
    overflow-x: overlay;
    padding-top: var(--padding-container);
    padding-bottom: var(--padding-container);
  }
  div.scrolly {
    overflow-y: auto;
    overflow-y: overlay;
    padding-left: var(--padding-container-large);
    padding-right: var(--padding-container-large);
  }
</style>

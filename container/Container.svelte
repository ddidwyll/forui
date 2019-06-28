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
    padding-top: var(--padding-small);
    padding-bottom: var(--padding-small);
  }
  div.scrolly {
    overflow-y: auto;
    overflow-y: overlay;
    padding-left: var(--padding-small);
    padding-right: var(--padding-small);
  }
</style>

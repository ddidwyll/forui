<div class:scrollx class:scrolly>
  <slot />
</div>

<script>
  export let scrollx = false
  export let scrolly = false
</script>

<style>
  div {
    box-sizing: border-box;
    width: var(--container-width-base);
    max-width: var(--container-max-width);
    height: 100%;
    max-height: 100%;
    background-color: var(--common-background-color-white);
    overflow: hidden;
    margin: 0 auto;
  }
  div.scrollx {
    overflow-x: auto;
    overflow-x: overlay;
    padding-top: var(--container-padding-x);
    padding-bottom: var(--container-padding-x);
  }
  div.scrolly {
    overflow-y: auto;
    overflow-y: overlay;
    padding-left: var(--container-padding-y);
    padding-right: var(--container-padding-y);
  }
  @media screen and (max-width: 900px) {
    div {
      width: var(--container-width-small);
    }
  }
</style>

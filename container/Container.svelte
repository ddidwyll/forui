<div class:scrollx class:scrolly class:small>
  <slot />
</div>

<script>
  export let scrollx = false
  export let scrolly = false
  export let small = false
</script>

<style>
  div {
    box-sizing: border-box;
    width: var(--container-width-base);
    max-width: var(--container-max-width);
    height: 100%;
    background-color: var(--common-background-color-white);
    overflow: hidden;
    margin: 0 auto;
  }
  div.small {
    height: var(--container-small-height);
    max-height: var(--container-small-max-height);
    min-height: var(--container-small-min-height);
    width: var(--container-small-width-base);
    max-width: var(--container-small-max-width);
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
    div.small {
      width: var(--container-small-width-small);
    }
  }
</style>

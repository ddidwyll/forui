<div class:center class:block class:right class:between class:wrap class:gutter {hidden}>
  <slot />
</div>

<script>
  export let center = false
  export let block = false
  export let right = false
  export let between = false
  export let wrap = false
  export let gutter = false
  export let hidden = false
</script>

<style>
  div {
    display: inline-flex;
    align-items: center;
    padding: 1px;
  }
  div.center {
    justify-content: center;
  }
  div.right {
    justify-content: flex-end;
  }
  div.between {
    justify-content: space-between;
  }
  div.block {
    display: flex;
  }
  div.wrap {
    flex-wrap: wrap;
  }
  div.wrap > :global(*) {
    margin-bottom: 3px;
  }
  div:not(.gutter) > :global(*:not(:last-child)) {
    border-top-right-radius: 0;
    border-bottom-right-radius: 0;
  }
  div:not(.gutter) > :global(*:not(:first-child)) {
    border-top-left-radius: 0;
    border-bottom-left-radius: 0;
  }
  div.gutter > :global(*) {
    margin-left: 3px;
    margin-right: 3px;
  }
  div > :global(:first-child) {
    margin-left: 0 !important;
  }
  div > :global(:last-child) {
    margin-right: 0 !important;
  }
</style>

<div>
  <slot />
</div>

<style>
  div {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    padding: 1px;
  }
  div > :global(*:not(:last-child)) {
    border-top-right-radius: 0;
    border-bottom-right-radius: 0;
  }
  div > :global(*:not(:first-child)) {
    border-top-left-radius: 0;
    border-bottom-left-radius: 0;
  }
  div > :global(*:not(:last-child):not(:first-child)) {
  }
</style>

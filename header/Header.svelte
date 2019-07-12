<header>
  <Container>
    <slot name="left" />
    <slot name="center" />
    <slot name="right" />
  </Container>
</header>

<script>
  import Container from '../container/Container.svelte'
</script>

<style>
  header {
    width: var(--header-width-base);
    height: var(--header-height-base);
    min-height: var(--header-height-base);
    max-height: var(--header-height-base);
    margin: 0 auto;
    background-color: var(--common-background-color-white);
    border-bottom: var(--container-border);
    box-shadow: var(--container-shadow);
  }
  header > :global(div) {
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  header > :global(div > *) {
    flex: 1 1;
    overflow: hidden;
    white-space: nowrap;
    text-overflow: ellipsis;
    padding: 2px 0;
  }
  header > :global(div > :last-child) {
    text-align: right;
  }
  header > :global(div > :not(:last-child):not(:first-child)) {
    text-align: center;
  }
  @media screen and (max-width: 900px) {
    header {
      box-sizing: border-box;
      padding: 0 var(--container-padding-y);
    }
  }
</style>

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
    width: var(--header-width);
    margin: 0 auto;
    height: var(--header-height);
    max-height: var(--header-height);
    background-color: var(--white-bg);
    border-bottom: var(--default-border);
    box-shadow: var(--shadow-large);
    margin-bottom: var(--margin-container);
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
</style>

<main>
  <Container scrolly>
    <slot />
  </Container>
</main>

<script>
  import Container from '../container/Container.svelte'
</script>

<style>
  main {
    padding: var(--container-padding-x) 0 0;
    flex-grow: 1;
    overflow: hidden;
  }
  main > :global(div) {
    box-shadow: var(--container-shadow);
    border: var(--container-border);
    padding-top: var(--container-padding-y);
    padding-bottom: var(--container-padding-y);
  }
</style>

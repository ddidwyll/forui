<main>
  <Container scrollx scrolly>
    <slot />
  </Container>
</main>

<script>
  import Container from '../container/Container.svelte'
</script>

<style>
  main {
    padding: var(--container-padding-x) 0 0;
  }
  main > :global(div) {
    box-shadow: var(--container-shadow);
    border: var(--container-border);
  }
</style>

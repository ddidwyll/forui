<main>
  <Container scrollx scrolly>
    <slot />
  </Container>
</main>

<script>
  import Container from '../container/Container.svelte'
</script>

<style>
  main > :global(div) {
    box-shadow: var(--shadow-large);
    border: var(--default-border);
  }
</style>

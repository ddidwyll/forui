<aside>
  <Container small scrolly>
    <slot />
  </Container>
</aside>

<script>
  export let open = false

  import Container from '../container/Container.svelte'
</script>

<style>
  aside {
    position: fixed;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    background-color: var(--common-background-color-light);
    display: flex;
    justify-content: center;
    align-items: center;
    padding-bottom: 10%;
  }
  aside > :global(*) {
    background-color: var(--common-background-color-white);
    box-shadow: var(--container-shadow);
    border: var(--container-border);
    padding-left: var(--container-padding-y);
    padding-right: var(--container-padding-y);
    padding-top: var(--container-padding-x);
    padding-bottom: var(--container-padding-x);
  }
</style>

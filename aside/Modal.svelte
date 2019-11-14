{#if open}
  <aside transition:fade on:click={e => close(e)}>
    <Container small scrolly>
      <slot />
    </Container>
  </aside>
{/if}

<script>
  export let open = false

  import Container from '../container/Container.svelte'
  import { fade } from 'svelte/transition'
  import { createEventDispatcher } from 'svelte'
  const dispatch = createEventDispatcher()

  const close = e => {
    if (e.target.nodeName !== 'ASIDE') return
    dispatch('close')
  }
</script>

<style>
  aside {
    background-color: #eeeeeeee;
    position: fixed;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    padding-bottom: 10%;
    z-index: 5;
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

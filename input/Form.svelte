<form on:submit {autocomplete}>
  <legend>{title}</legend>
  {#each fields as { name, label, type, required, min, max, autofocus, disabled, hidden, simple, clean, block, small, large }}
    <Input
      {label}
      {type}
      {required}
      {min}
      {max}
      {autofocus}
      {disabled}
      {hidden}
      {simple}
      {clean}
      {block}
      {small}
      {large}
      on:input={e => input(e, name)}
      value={result[name]} />
  {/each}
  <slot name="buttons" />
</form>

<script>
  export let title = ''
  export let fields = []
  export let autocomplete = true

  import { createEventDispatcher } from 'svelte'
  import Input from './Input.svelte'

  let result = {}
  const dispatch = createEventDispatcher()
  const input = (e, key) => {
    result[key] = e.detail
    result = { ...result }
    dispatch('input', result)
  }
</script>

<style>
  form {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: stretch;
  }
  legend {
    font-size: 1.2rem;
    margin-bottom: 6px;
    text-align: center;
  }
  form > :global(*):not(legend) {
    margin: 8px 0;
  }
  form > :global(:last-child) {
    margin-bottom: 0;
  }
</style>

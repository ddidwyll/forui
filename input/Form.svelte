<svelte:window on:keydown={e => escape(e)} />

<form on:submit|preventDefault={() => null} {autocomplete} noValidate>
  <div>
    {#if close}
      <Button
        label={close}
        danger
        small
        center
        on:click={() => dispatch('close')} />
    {/if}
    <legend>{title}</legend>
    {#if submit}
      <Button
        label={submit}
        success
        small
        center
        on:click={() => ok()}
        disabled={hasErrors} />
    {/if}
  </div>
  {#each fields as { name, label, type, required, min, max, autofocus, disabled, hidden, simple, clean, block, small, large, hints }}
    <Input
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
      {hints}
      {large}
      label={$errors[name] || label}
      invalid={$errors[name]}
      valid={$errors[name] === ''}
      on:blur={() => needCheck(name)}
      on:focus={() => needCheck(name, false)}
      on:input={e => input(e, name)}
      on:enter={() => ok()}
      value={result[name]} />
  {/each}
  <slot name="buttons" />
</form>

<script>
  export let title = ''
  export let fields = []
  export let autocomplete = true
  export let close = ''
  export let submit = ''
  export let result = {}

  import { createEventDispatcher } from 'svelte'
  import Button from '../button/Button.svelte'
  import Input from './Input.svelte'
  import { writable } from 'svelte/store'

  const dispatch = createEventDispatcher()
  const input = (e, key) => {
    result[key] = e.detail
    result = { ...result }
    dispatch('input', result)
  }
  const ok = () => ($hasErrors ? null : dispatch('submit', result))

  const { subscribe, update } = writable({ needInit: true })
  const errors = { subscribe }
  const needCheck = (field, need = true) =>
    update(errors => {
      errors.needInit = false
      if (need) errors[field] = ''
      else delete errors[field]
      return { ...errors }
    })
  $: {
    fields.forEach(field => {
      const key = field.name
      if ($errors[key] === undefined) return
      update(errors => {
        if (!errors || errors[key] === undefined) return errors
        if (field.required && (!result[key] && result[key] !== 0)) {
          errors[key] = field.required
        }
        return { ...errors }
      })
    })
  }

  $: hasErrors =
    $errors.needInit || Object.values($errors).some(error => !!error)

  const escape = e => {
    if (e.keyCode !== 27) return
    dispatch('close')
  }
</script>

<style>
  form {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: stretch;
  }
  div {
    display: flex;
    justify-content: space-between;
  }
  div > :global(button) {
    min-width: 100px;
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
  @media screen and (max-width: 600px) {
    div {
      flex-wrap: wrap;
    }
    legend {
      width: 100%;
      order: -1;
    }
  }
</style>

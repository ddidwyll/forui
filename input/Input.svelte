<input
  type={type || 'text'}
  value={format(value)}
  min={range(min)}
  max={range(max)}
  class:error
  class:valid
  class:flat
  class:clean
  placeholder={label || ''}
  aria-label={label || ''}
  title={label || ''}
  {disabled}
  {hidden}
  {required}
  on:input={e => bubble(e)}
  on:change={e => bubble(e)}
  on:keydown={e => enter(e)} />

<script>
  import { createEventDispatcher } from 'svelte'
  const dispatch = createEventDispatcher()

  export let label = null
  export let disabled = false
  export let hidden = false
  export let error = false
  export let valid = false
  export let flat = false
  export let clean = false
  export let required = false
  export let type = 'text'
  export let value = ''
  export let min = null
  export let max = null

  const format = value => {
    switch (type) {
      case 'date':
        return +value > 0
          ? new Date(+value)
              .toLocaleDateString('en-GB')
              .split('/')
              .reverse()
              .join('-')
          : ''
      case 'number':
        return +value || null
      default:
        return value || ''
    }
  }

  const range = value => {
    switch (type) {
      case 'date':
        return value ? format(value) : ''
      case 'number':
        return value || ''
      default:
        return ''
    }
  }

  const bubble = e => {
    const target = e.target.value
    let value

    switch (type) {
      case 'date':
        value = target ? new Date(target).getTime() : null
        break
      case 'number':
        value = +target || 0
        break
      default:
        value = target
    }
    dispatch(e.type, value)
  }

  const enter = e => {
    if (e.keyCode !== 13) return
    e.preventDefault()
    dispatch('enter')
  }
</script>

<style>
  input {
    border: var(--button-border);
    border-radius: var(--button-border-radius);
    height: var(--button-height);
    color: var(--primary-txt);
    box-sizing: border-box;
    vertical-align: middle;
    padding: 0 var(--padding-xsmall);
    box-shadow: inset 0 0 5px 0 var(--shadow-trans-color);
    font-size: var(--input-font-size);
    outline: none;
    cursor: text;
  }
  input.clean,
  input.flat {
    box-shadow: none;
  }
  input.clean {
    border-width: 0;
    border-bottom-width: 2px;
    border-radius: 1px;
    padding-left: 5px;
    padding-right: 5px;
  }
  input:hover,
  input:focus {
    border-color: var(--border-dark-color);
  }
  input.error {
    border-color: var(--button-bg-danger);
  }
  input.valid {
    border-color: var(--button-bg-success);
  }
  ::placeholder {
    opacity: 0.8;
  }
</style>

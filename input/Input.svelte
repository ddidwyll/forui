<div class:block class:small>
  <input
    bind:this={input}
    {type}
    class:valid
    class:invalid
    class:clean
    class:simple
    value={format(value)}
    min={min ? range(min) : null}
    max={max ? range(max) : null}
    maxLength={type === 'text' && max ? max : null}
    placeholder={label}
    aria-label={label}
    {disabled}
    {hidden}
    {required}
    {autofocus}
    on:focus
    on:blur
    on:input={e => bubble(e)}
    on:change={e => bubble(e)}
    on:keydown={e => enter(e)} />
  <label class:active={value || value === 0}>
    {label || ''}
    {#if type === 'text'}{max ? `(${length}/${max})` : ''}{/if}
  </label>
  {#if hints && filtered.length && !~hints.indexOf(value)}
    <figure>
      {#each filtered as hint}
        <span on:click={() => bubbleEmu(hint)}>{hint}</span>
      {/each}
    </figure>
  {/if}
  <slot />
</div>

<script>
  import { createEventDispatcher } from 'svelte'
  const dispatch = createEventDispatcher()

  export let label = null
  export let disabled = false
  export let hidden = false
  export let valid = false
  export let invalid = false
  export let clean = false
  export let simple = false
  export let block = false
  export let small = false
  export let large = false
  export let required = false
  export let hints = null
  export let type = 'text'
  export let value = ''
  export let min = null
  export let max = null
  export let autofocus = false

  let input = null
  let length = 0

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
        value = value || ''
        length = value.length
        return max ? value.slice(0, max) : value
    }
  }

  const range = value => {
    switch (type) {
      case 'date':
        return value ? format(value) : ''
      case 'number':
        return value || ''
      default:
        return null
    }
  }

  const bubbleEmu = value => {
    if (input) input.focus()
    bubble({ type: 'input', target: { value } })
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
        value = max ? target.slice(0, max) : target
    }
    dispatch(e.type, value)
  }

  const enter = e => {
    if (e.keyCode !== 13) return
    e.preventDefault()
    dispatch('enter')
  }

  $: filtered = (hints || []).filter(
    hint => ~hint.toUpperCase().indexOf((value || '').toUpperCase())
  )
</script>

<style>
  div {
    position: relative;
    display: inline-flex;
    align-items: center;
    height: var(--input-height-base);
    min-width: var(--input-min-width);
    vertical-align: middle;
    cursor: text;
  }
  div > :global(*) {
    cursor: inherit;
  }
  input {
    padding: var(--control-padding-base);
    color: var(--primary-txt);
    font-size: var(--input-font-size);
    line-height: var(--input-line-height-base);
    height: 100%;
    min-width: var(--input-min-width);
    background-color: var(--input-background-color-base);
    border: var(--input-border);
    border-color: var(--input-border-color-primary);
    border-radius: var(--input-border-radius);
    box-shadow: var(--input-shadow);
    box-sizing: border-box;
    outline: none;
    flex-grow: 1;
  }
  div.small,
  div.small > input {
    height: var(--input-height-small);
    line-height: var(--input-line-height-small);
  }
  input:hover:not(:disabled),
  input:focus {
    border-color: var(--input-border-color-dark);
    background-color: var(--input-background-color-focus);
  }
  input:focus:not(.clean) {
    outline-offset: -4px;
    outline: 0px dashed var(--input-border-color-primary);
  }
  input.valid:not(#hack) {
    border-color: var(--input-border-color-secondary);
  }
  input.invalid:not(#hack) {
    border-color: var(--input-border-color-tertiary);
  }
  input.clean {
    border-width: 0;
    border-bottom-width: 2px;
    border-radius: 1px;
    box-shadow: none;
    background-color: transparent;
  }
  input:disabled {
    cursor: not-allowed;
    opacity: 0.7;
  }
  ::placeholder {
    opacity: 0;
  }
  label {
    position: absolute;
    top: var(--common-border-width-base);
    left: 0.8rem;
    line-height: var(--input-line-height-base);
    pointer-events: none;
    opacity: 0.7;
  }
  label.active,
  input:focus + label {
    color: var(--input-border-color-dark);
    line-height: 1;
    top: -18%;
    background: var(--input-background-color-focus);
    opacity: 1;
  }
  input.simple + label.active,
  input.simple:focus + label {
    opacity: 0;
  }
  div > :global(:last-child:not(label):not(figure)) {
    position: absolute;
    right: 0;
    cursor: auto;
  }
  div > :global(svg:not(#hack)) {
    right: 0.8rem;
    pointer-events: none;
  }
  div > :global(button:not(.active)) {
    cursor: auto;
    box-shadow: none;
    cursor: pointer;
    border-top-left-radius: 0px;
    border-bottom-left-radius: 0px;
  }
  div.block {
    display: flex;
  }
  :global(::-webkit-inner-spin-button),
  :global(::-webkit-outer-spin-button) {
    -webkit-appearance: none;
    margin: 0;
  }
  figure {
    background-color: var(--input-background-color-focus);
    padding: var(--control-padding-base);
    display: flex;
    border: var(--input-border);
    border-color: var(--input-border-color-dark);
    border-radius: var(--input-border-radius);
    border-width: 0;
    flex-direction: column;
    margin: 0;
    position: absolute;
    top: calc(100% - 2px);
    left: 0;
    right: 0;
    max-height: 0;
    overflow-y: auto;
    overflow-x: hidden;
    z-index: 2;
  }
  input:focus + label + figure,
  figure:hover {
    max-height: 100px;
    border-width: 1px;
    box-shadow: var(--input-shadow);
  }
  figure > span {
    cursor: pointer;
  }
</style>

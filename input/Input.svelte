<div class:block class:small class:large {hidden}>
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
    {required}
    {autofocus}
    on:focus
    on:blur
    on:input={e => bubble(e)}
    on:change={e => bubble(e)}
    on:keydown={e => enter(e)} />
  <label class:active={value || value === 0}>
    {label || ''}
    {#if type === 'text' && max && length}
      <sup>({`${length}/${max}`})</sup>
    {/if}
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
  export let filter = null
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
        const filtered = filter ? value.replace(filter, '') : value
        length = filtered.length
        return max ? filtered.slice(0, max) : filtered
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

    switch (type) {
      case 'date':
        value = target ? new Date(target).getTime() : null
        break
      case 'number':
        value = +target
        break
      default:
        const filtered = filter ? target.replace(filter, '') : target
        value = max ? filtered.slice(0, max) : filtered
    }
    e.target.value = format(value)
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
  div.large,
  div.large > input {
    height: var(--input-height-large);
    line-height: var(--input-line-height-large);
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
    top: 0;
    left: 0.8rem;
    line-height: var(--input-line-height-base) ;
    height: inherit;
    pointer-events: none;
    opacity: 0.7;
    white-space: nowrap;
    overflow: hidden;
    max-width: 80%;
    font-weight: normal;
  }
  div.small > label {
    line-height: var(--input-line-height-small);
  }
  div.large > label {
    line-height: var(--input-line-height-large);
  }
  label.active:not(#hack),
  input:focus + label {
    color: var(--input-border-color-dark);
    top: -50%;
    opacity: 1;
    background: linear-gradient(0deg, transparent 40%, var(--input-background-color-base) 40%, var(--input-background-color-base) 52%, transparent 52%);
  }
  input:hover:not(:disabled) + label:not(#hack),
  input:focus + label:not(#hack) {
    background: linear-gradient(0deg, transparent 40%, var(--input-background-color-focus) 40%, var(--input-background-color-focus) 52%, transparent 52%);
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
  label > sup {
    top: -0.2em;
  }
</style>

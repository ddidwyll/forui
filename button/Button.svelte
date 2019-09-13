<button
  on:click
  aria-label={label}
  title={label}
  {disabled}
  {hidden}
  {style}
  class:active
  class:success
  class:inverse
  class:danger
  class:clean
  class:large
  class:small
  class:image
  class:block>
  <slot>{label || ''}</slot>
</button>

<script>
  export let image = null
  export let label = null
  export let disabled = false
  export let hidden = false
  export let active = false
  export let success = false
  export let inverse = false
  export let danger = false
  export let clean = false
  export let small = false
  export let large = false
  export let block = false
  export let style = null
</script>

<style>
  button {
    display: inline-flex;
    align-items: baseline;
    justify-content: space-between;
    height: var(--button-height-base);
    padding: var(--control-padding-base);
    font-size: var(--button-font-size-base);
    font-weight: var(--button-font-weight-base);
    line-height: var(--control-line-height-base);
    text-transform: var(--button-text-transform);
    letter-spacing: var(--button-letter-spacing);
    color: var(--button-color-primary-base);
    background-color: var(--button-background-color-primary-base);
    border: var(--button-border);
    border-color: var(--button-border-color-primary);
    border-radius: var(--button-border-radius);
    box-shadow: var(--button-shadow-base)
      var(--button-shadow-color-primary-base);
    outline: none;
    vertical-align: middle;
    overflow: hidden;
    word-break: break-all;
  }
  button:disabled {
    opacity: 0.6;
    cursor: not-allowed;
  }
  button:focus:not(.active) {
    outline-offset: -4px;
    outline: 0px dashed var(--button-border-color-primary);
  }
  button:hover:not(:disabled):not(.active) {
    opacity: 0.8;
    box-shadow: none;
  }
  button:active:not(.inverse):not(.clean),
  button.active:not(.inverse):not(:disabled) {
    outline: none;
    box-shadow: var(--button-shadow-inset)
      var(--button-shadow-color-primary-base);
    background-color: var(--common-background-color-white);
    color: var(--button-color-primary-light);
  }
  button.active {
    cursor: default;
  }
  button.danger {
    border-color: var(--button-border-color-tertiary);
    background-color: var(--button-background-color-tertiary-base);
  }
  button.success {
    border-color: var(--button-border-color-secondary);
    background-color: var(--button-background-color-secondary-base);
  }
  button.inverse {
    background-color: var(--button-background-color-primary-inverse);
    color: var(--common-color-white);
    box-shadow: var(--button-shadow-base)
      var(--button-shadow-color-primary-dark);
    border-color: transparent;
  }
  button.inverse > :global(svg) {
    fill: var(--common-color-white);
  }
  button.inverse:active:not(#hack):not(:disabled),
  button.inverse.active:not(:disabled) {
    background-color: var(--button-background-color-primary-inverse);
    color: var(--common-color-white);
    opacity: 0.7;
    box-shadow: var(--button-shadow-inverse)
      var(--button-shadow-color-primary-dark);
  }
  button.success.inverse:active:not(#hack):not(:disabled),
  button.success.inverse.active:not(:disabled),
  button.inverse.success {
    background-color: var(--button-background-color-secondary-inverse);
  }
  button.danger.inverse:active:not(#hack):not(:disabled),
  button.danger.inverse.active:not(:disabled),
  button.inverse.danger {
    background-color: var(--button-background-color-tertiary-inverse);
  }
  button.clean {
    position: relative;
    border-color: transparent;
    background-color: transparent;
    box-shadow: none;
  }
  button.clean:hover:not(:disabled):not(.active) {
    top: 1px;
  }
  button.clean.active {
    border-radius: 1rem;
  }
  button.small {
    height: var(--button-height-small);
    line-height: var(--button-line-height-small);
    padding: var(--control-padding-small);
  }
  button.large {
    height: var(--button-height-large);
    line-height: var(--button-line-height-large);
    padding: var(--control-padding-large);
  }
  button.block {
    display: flex;
  }
  button > :global(img) {
    height: 9px;
    width: auto;
  }
</style>

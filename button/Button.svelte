<button
  on:click
  aria-label={label}
  title={label}
  {disabled}
  {hidden}
  class:active
  class:success
  class:inverse
  class:danger
  class:flat
  class:icon
  class:clean>
  <slot />
</button>

<script>
  export let label = ''
  export let disabled = false
  export let hidden = false
  export let active = false
  export let success = false
  export let inverse = false
  export let danger = false
  export let flat = false
  export let icon = false
  export let clean = false
</script>

<style>
  button {
    height: var(--button-height-base);
    font-size: var(--button-font-size-base);
    text-transform: var(--button-text-transform);
    color: var(--button-color-primary-base);
    background-color: var(--button-background-color-primary-base);
    border: var(--button-border);
    border-color: var(--button-border-color-primary-base);
    border-radius: var(--button-border-radius);
    padding: 0 0.8rem;
    outline: none;
    font-weight: var(--font-weight);
    box-shadow: var(--button-shadow);
    text-shadow: 0 0 0 var(--dark-bg);
    vertical-align: middle;
    letter-spacing: 1px;
  }
  button:hover:not(:disabled) {
    opacity: 0.8;
    box-shadow: none;
    border-color: transparent;
  }
  button.active {
    pointer-events: none;
    border-color: var(--shadow-trans-color);
    box-shadow: inset 0 0 5px 0 var(--shadow-trans-color);
  }
  button.inverse {
    background-color: var(--button-bg-inverse);
  }
  button.inverse.success {
    background-color: var(--button-bg-inverse-success);
  }
  button.inverse.danger {
    background-color: var(--button-bg-inverse-danger);
  }
  button.success {
    background-color: var(--button-bg-success);
  }
  button.danger {
    background-color: var(--button-bg-danger);
  }
  button.inverse {
    border-color: var(--border-dark-color);
    color: var(--white-txt);
  }
  button.flat:not(.active) {
    box-shadow: none;
  }
  button.flat.success:not(.active) {
    border-color: var(--button-bg-success);
  }
  button.flat.danger:not(.active) {
    border-color: var(--button-bg-danger);
  }
  button.active {
    pointer-events: none;
    border-color: var(--shadow-trans-color);
    box-shadow: inset 0 0 5px 0 var(--shadow-trans-color);
  }
  button.active.inverse {
    box-shadow: inset 0 0 0 1px var(--trans-bg);
  }
  button:disabled {
    opacity: 0.4;
    cursor: not-allowed;
  }
  button > :global(svg) {
    fill: var(--button-txt);
    max-height: 24px;
    max-width: 24px;
  }
  button.inverse > :global(svg) {
    fill: var(--white-txt);
  }
  button.icon {
    padding: calc(var(--padding-xsmall) * 0.55) var(--padding-xsmall);
  }
  button.clean:not(.active) {
    border-color: transparent;
  }
</style>

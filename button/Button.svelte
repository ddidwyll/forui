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
  class:icon>
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
</script>

<style>
  button {
    height: 40px;
    font-size: var(--button-font-size);
    text-transform: var(--button-case);
    color: var(--primary-txt);
    background-color: var(--button-bg);
    border: var(--button-border);
    border-radius: var(--button-border-radius);
    padding: var(--padding-xsmall) var(--padding-small);
    outline: none;
    font-weight: var(--font-weight-bolder);
    box-shadow: var(--button-shadow);
    transition: all 0.3s ease-in-out;
  }
  button:hover:not(:disabled) {
    opacity: 0.8;
    box-shadow: none;
    transform: translateY(1px);
  }
  button:active {
    transform: translateY(2px);
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
    opacity: 0.6;
    cursor: not-allowed;
  }
  button > :global(svg) {
    fill: var(--primary-txt);
  }
  button.inverse > :global(svg) {
    fill: var(--white-txt);
  }
  button.icon:not(.hack) {
    padding: calc(var(--padding-xsmall) / 2) var(--padding-xsmall);
  }
  /*
  button:not(.icon).success {
    background-color: #37c936;
    border-color: #37c936;
    color: #fff;
  }
  button.icon.success > :global(svg) {
    fill: #4faf4e;
  }
  button:not(.icon).success:hover,
  button:not(.icon).success:focus {
    color: #fff;
    background-color: #4bce4a;
    border-color: #4bce4a;
    box-shadow: none;
  }
  button:not(.icon).success:active {
    background-color: #32b531;
    border-color: #32b531;
    box-shadow: none;
  }
  button:not(.icon).success.active {
    background-color: #32b531;
    border-color: #32b531;
  }
  button:not(.icon).success.active:hover,
  button:not(.icon).success.active:focus {
    background-color: #32b531;
    border-color: #32b531;
    box-shadow: none;
  }
  button:not(.icon).success.inverse {
    background-color: #ebfaeb;
    color: #37c936;
    border-color: transparent;
    box-shadow: none;
  }
  button:not(.icon).success.inverse:hover,
  button:not(.icon).success.inverse:focus {
    background-color: #d7f4d7;
    color: #32b531;
    border-color: transparent;
  }
  button:not(.icon).success[disabled] {
    background-color: #37c936;
    border-color: #37c936;
    opacity: 0.35;
  }
  button:not(.icon).success[disabled]:hover,
  button:not(.icon).success[disabled]:focus {
    background-color: #37c936;
    border-color: #37c936;
  }
  button:not(.icon).danger {
    color: #ffffff;
    background-color: #ff3c7e;
    border-color: #ff3c7e;
  }
  button.icon.danger > :global(svg) {
    fill: #c18899;
  }
  button:not(.icon).danger:hover,
  button:not(.icon).danger:focus {
    color: #ffffff;
    background-color: #ff568f;
    border-color: #ff568f;
    box-shadow: none;
  }
  button:not(.icon).danger:active {
    background-color: #ff236d;
    border-color: #ff236d;
    box-shadow: none;
  }
  button:not(.icon).danger.active {
    background-color: #ff236d;
    border-color: #ff236d;
  }
  button:not(.icon).danger.active:hover,
  button:not(.icon).danger.active:focus {
    background-color: #ff236d;
    border-color: #ff236d;
    box-shadow: none;
  }
  button:not(.icon).danger.inverse {
    background-color: #ffeff4;
    color: #ff3c7e;
    border-color: transparent;
    box-shadow: none;
  }
  button:not(.icon).danger.inverse:hover,
  button:not(.icon).danger.inverse:focus {
    background-color: #ffd5e3;
    color: #ff236d;
    border-color: transparent;
  }
  button:not(.icon).danger.disabled {
    background-color: #ff3c7e;
    border-color: #ff3c7e;
    opacity: 0.35;
  }
  button:not(.icon).danger.disabled:hover,
  button:not(.icon).danger.disabled:focus {
    background-color: #ff3c7e;
    border-color: #ff3c7e;
  }
  button.flat:not(.hack) {
    box-shadow: none;
    border-color: transparent;
  }*/
</style>

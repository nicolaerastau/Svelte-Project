<script>
  export let buttonSecondary = false;
  export let buttonPrimary = false;
</script>

<style>
  .buttonPrimary {
    font: inherit;
    padding: 0.15rem 0.5rem;
    background: #d10057;
    border: 0.5px solid rgb(6, 166, 194);
    color: white;
    cursor: pointer;
    margin-top: 10px;
  }
  .buttonSecondary {
    background: rgb(6, 166, 194);
    font: inherit;
    padding: 0.15rem 0.5rem;
    border: 0.5px solid #d10057;
    color: white;
    cursor: pointer;
  }

  @media (max-width: 465px) {
    .buttonSecondary {
      margin-top: 10px;
    }
  }

  button:hover:hover,
  button:active {
    box-shadow: 1px 1px 6px rgba(0, 0, 0, 0.26);
  }
</style>

<button class:buttonSecondary class:buttonPrimary on:click>
  <slot />
</button>

<script>
  import { currentPage } from "./stores";
  import Button from "./Button.svelte";
</script>

<slot />
<div class="slideNumber">{$currentPage + 1}</div>
<Button on:click={() => ($currentPage = undefined)}>Back to Contents</Button>

<style>
  .slideNumber {
    position: absolute;
    top: 0;
    right: 0;
    padding: 0.5rem;
    background-color: rgba(0, 0, 0, 0);
    color: white;
    font-size: 1.5rem;
    font-weight: bold;
    text-align: center;
  }
</style>

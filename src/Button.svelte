<script>
  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();
</script>

<button
  on:click={(event) => {
    dispatch("click", event);
  }}><slot /></button
>

<style>
  button {
    color: white;
    background-color: transparent;
    border: none;
    padding: 0;
    margin: 0;
    position: relative;
  }

  button:hover {
    text-decoration: underline;
    cursor: pointer;
  }

  button:active {
    background-color: transparent;
  }
</style>

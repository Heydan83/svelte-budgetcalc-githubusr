<script>
  import { getContext, createEventDispatcher } from "svelte";

  export let name = "";
  export let value = "";
  export let text = "";
  export let checked = false;
  export let selectedValue = "none";

  let dispatch = createEventDispatcher();
  let formSelected = getContext("form");

  function checkSelection(formName) {
    dispatch("selected");
    formSelected(formName);
  }
</script>

<style>
  label {
    font-size: 20px;
  }
</style>

<div>
  <label>
    {#if checked}
      ->
      <input
        type="radio"
        checked
        {name}
        {value}
        bind:group={selectedValue}
        on:change={() => checkSelection(value)} />
    {:else}
      <input
        type="radio"
        {name}
        {value}
        bind:group={selectedValue}
        on:change={() => checkSelection(value)} />
    {/if}
    {text}
    <br />
    <br />
  </label>
</div>

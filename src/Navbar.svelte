<script>
  import SelectForm from "./SelectForm.svelte";

  export let showForm;
  export let formShowed = "";

  let isArrowClick = false;

  function closeMenu() {
    isArrowClick = !isArrowClick;
  }
</script>

<nav class="nav">
  <div class="nav-center">
    <button
      type="button"
      class="nav-btn"
      on:click={() => (isArrowClick = !isArrowClick)}>
      <i
        class="fas"
        class:fa-angle-down={isArrowClick}
        class:fa-angle-right={!isArrowClick} />
    </button>
    {#if isArrowClick}
      <SelectForm {formShowed} on:selected={closeMenu} />
    {/if}
    {#if formShowed === 'budget'}
      <h1 class="nav-title">Budget Calculator</h1>
      <button type="button" class="nav-btn" on:click={showForm}>
        <i class="far fa-plus-square" />
        Add Item
      </button>
    {:else if formShowed === 'github'}
      <h1 class="nav-title">Github Users</h1>
    {:else}
      <h1 class="nav-title">Github Users Await</h1>
    {/if}
  </div>
</nav>

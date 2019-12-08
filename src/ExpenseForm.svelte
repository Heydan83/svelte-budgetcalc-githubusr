<script>
   // import { onMount, onDestroy, beforeUpdate, afterUpdate } from 'svelte';

  // onMount(() => {
  //   console.log("form has mounted");
  // });
  // beforeUpdate(() => {
  //   console.count("before update");
  // });
  // afterUpdate(() => {
  //   console.count("after update");
  // });
  // onDestroy(() => {
  //   console.log("form is hidden");
  // });
  // Components
  import Title from "./Title.svelte";

  // Props
  export let name = "";
  export let amount = null;
  export let addExpense;
  export let isEditing;
  export let editExpense;
  export let hideForm;

  // Reactivity
  // In javascript a truthy value is considered TRUE when encountered un boolean context.
  $: isEmpty = !name || !amount;

  // Functions
  function handleSubmit() {
    if (isEditing) {
      editExpense({ name, amount })
    } else {
      addExpense({ name, amount });
    }

    name = "";
    amount = null;
    hideForm();
  }
</script>

<section class="form">
  <Title title="Add Expense" />
  <form class="expense-form" on:submit|preventDefault={handleSubmit}>
    <div class="form-control">
      <label for="name">Name</label>
      <input type="text" id="name" bind:value={name} />
    </div>
    <div class="form-control">
      <label for="amount">Amount</label>
      <input type="number" id="amount" bind:value={amount} />
    </div>
    {#if isEmpty}
      <p class="form-empty">Please fill out all form fields</p>
    {/if}
    <button
      type="submit"
      class="btn btn-block"
      class:disabled={isEmpty}
      disabled={isEmpty}>
      {#if isEditing}
        Edit Expense
      {:else}
        Add Expense
      {/if}
    </button>
    <button type="button" class="close-btn" on:click={hideForm}>
      <div>
        <i class="fas fa-times" />Close
      </div>
    </button>
  </form>
</section>

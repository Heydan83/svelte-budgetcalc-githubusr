<script>
  // Modules
  import { blur, slide, scale, fade, fly } from "svelte/transition";
  import { quintOut } from "svelte/easing";
  import { getContext, createEventDispatcher } from "svelte";

  // Props
  export let id;
  export let name = "";
  export let amount = 0;
  // export let removeExpense;

  // Variables
  let displayAmount = false;
  let dispatch = createEventDispatcher();

  // Functions
  function toggleAmount() {
    displayAmount = !displayAmount;
  }

  const removeExpense = getContext("remove");
  const setModifiedExpense = getContext("modify");
</script>

<article class="single-expense">
  <div class="expense-info">
    <h2>
      {name}
      <button class="amount-btn" on:click={toggleAmount}>
        <i class="fas fa-caret-down" />
      </button>
    </h2>
    {#if displayAmount}
      <h4 transition:slide>Amount : ${amount}</h4>
      <!-- <h4 transition:blur>Amount : ${amount}</h4> -->
      <!-- <h4 transition:scale>Amount : ${amount}</h4> -->
      <!-- <h4 transition:fade>Amount : ${amount}</h4> -->
      <!-- <h4
        in:fly={{ x: 100, y: 100, duration: 500, delay: 50, easing: quintOut }}
        out:slide>
        Amount : ${amount}
      </h4> -->
    {/if}
  </div>
  <div class="expense-buttons">
    <button
      class="expense-btn edit-btn"
      on:click={() => setModifiedExpense(id)}>
      <i class="fas fa-pen" />
    </button>
    <!-- <button class="expense-btn delete-btn" on:click={removeExpense(id)}> -->
    <button class="expense-btn delete-btn" on:click={() => removeExpense(id)}>
      <i class="fas fa-trash" />
    </button>
    <!-- <button class="expense-btn delete-btn" on:click={() => dispatch('delete', {id, name: 'hello from expenses'})}>
      <i class="fas fa-trash" />
    </button> -->
  </div>
</article>

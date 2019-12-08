<script>
  // Modules
  import { setContext, onMount, afterUpdate } from "svelte";
  import Github from "./Github.svelte";
  import GithubAwait from "./GithubAwait.svelte";

  // const state = {
  //   name: 'simplen name',
  //   remove: removeExpense
  // }

  // Components
  import Navbar from "./Navbar.svelte";
  import ExpensesList from "./ExpensesList.svelte";
  import Totals from "./Totals.svelte";
  import ExpenseForm from "./ExpenseForm.svelte";
  import Modal from "./Modal.svelte";

  // Data
  // import expensesData from "./expenses";

  // Variables
  let expenses = [];

  // Set editing variables
  let setName = "";
  let setAmount = null;
  let setId = null;
  let formShowed = "budget";

  // Toggle form variables
  let isFormOpen = false;

  // Reactive
  $: isEditing = setId ? true : false;

  $: total = expenses.reduce((acc, curr) => {
    return (acc += curr.amount);
  }, 0);

  // Funtions
  function showForm() {
    isFormOpen = true;
  }

  function hideForm() {
    isFormOpen = false;
    setName = "";
    setAmount = null;
    setId = null;
  }

  function removeExpense(id) {
    expenses = expenses.filter(item => item.id !== id);
  }

  function clearExpenses() {
    expenses = [];
  }

  function addExpense({ name, amount }) {
    let expense = { id: Math.random() * Date.now(), name, amount };
    expenses = [expense, ...expenses];
  }

  function setModifiedExpense(id) {
    let expense = expenses.find(item => item.id === id);
    setId = expense.id;
    setName = expense.name;
    setAmount = expense.amount;
    showForm();
  }

  function editExpense({ name, amount }) {
    expenses = expenses.map(item => {
      return item.id === setId ? { ...item, name, amount } : { ...item };
    });

    setId = null;
    setName = null;
    setAmount = "";
  }

  function formSelected(formName) {
    formShowed = formName;
  }

  // function deleteExpense(event) {
  //   const { id, name } = event.detail;

  //   removeExpense(id);
  // }

  // Context
  setContext("remove", removeExpense);
  setContext("modify", setModifiedExpense);
  setContext("form", formSelected);
  // setContext("state", state);

  // Local storage
  function setLocalStorage() {
    localStorage.setItem("expenses", JSON.stringify(expenses));
  }

  onMount(() => {
    expenses = localStorage.getItem("expenses")
      ? JSON.parse(localStorage.getItem("expenses"))
      : [];
  });

  afterUpdate(() => {
    setLocalStorage();
  });
</script>

<Navbar {showForm} formShowed={formShowed} />
<main class="content">
  {#if formShowed === 'budget'}
    {#if isFormOpen}
      <Modal>
        <ExpenseForm
          {addExpense}
          name={setName}
          amount={setAmount}
          {isEditing}
          {editExpense}
          {hideForm} />
      </Modal>
    {/if}
    <Totals title="Total Expenses" {total} />
    <ExpensesList {expenses} />
    <button
      type="button"
      class="btn btn-primary btn-block"
      on:click={clearExpenses}>
      Clear Expenses
    </button>
  {:else if formShowed === 'github'}
    <Github />
  {:else}
    <GithubAwait />
  {/if}
</main>
<!-- <Modal>
  <h1 slot="header">Hello world</h1>
  <p slot="footer">
    Lorem ipsum dolor sit amet consectetur, adipisicing elit. Ullam aliquam alias minus officia velit dolor accusamus facilis ducimus quia provident!
  </p>
</Modal> -->

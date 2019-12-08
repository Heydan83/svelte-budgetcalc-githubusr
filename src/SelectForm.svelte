<script>
  import { fly } from "svelte/transition";
  import RadioButton from "./RadioButton.svelte";

  export let selectedValue = '';
  export let formShowed = '';

  let forms = [
    { value: "budget", text: "Budget Calculator", checked: false },
    { value: "github", text: "Github Users", checked: false },
    { value: "githubawait", text: "Github Users Await", checked: false }
  ];

  forms.forEach(item => {
    if (item.value === formShowed) {
      item.checked = true;
    }
  });

</script>

<div class="select-form" transition:fly={{ y: -200 }}>
  <div>
    {#each forms as form, index (form.value)}
      <RadioButton name="selectForm" value={form.value} text={form.text} bind:selectedValue={selectedValue} checked={form.checked} on:selected />
    {/each}
    <!-- <button type="submit" class="btn btn-primary">Confirm</button> -->
  </div>
</div>

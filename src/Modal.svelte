<script>
  import { blur, fade, fly } from 'svelte/transition';
</script>

<div class="modal-container" in:blur out:fade>
  <div class="modal-content" transition:fly={{ y:200 }}>
    <!-- <h3>Hello from modal</h3>
    <h2>bottom heading</h2>
    <slot></slot> -->
    <!-- <slot name="header"></slot>
    <slot name="footer"></slot> -->
    <slot><!-- optional fallback --></slot>
  </div>
</div>
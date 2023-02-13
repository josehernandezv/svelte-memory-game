<script>
  import coverSrc from "../assets/cover.png";
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();

  export let src;
  export let flipped = false;
</script>

<!-- svelte-ignore a11y-click-events-have-key-events -->
<div class="card" on:click={() => dispatch("flip")}>
  <!-- <img src={coverSrc} alt="Carta" /> -->
  <img src={flipped ? src : coverSrc} alt="Carta" />
</div>

<style>
  .card {
    position: relative;
    border: 10px solid transparent;
  }
  .card:hover {
    border-image: url(../assets/cardBorder.png) 30 round;
    overflow: hidden;
    cursor: pointer;
  }
  .card img {
    filter: drop-shadow(12px 12px 0 #200060);
  }
</style>

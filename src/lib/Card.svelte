<script>
  import coverSrc from "../assets/cover.png";
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();

  export let src;
  export let flipped = false;
</script>

<!-- svelte-ignore a11y-click-events-have-key-events -->
<div class="card" class:flipped on:click={() => dispatch("flip")}>
  <img {src} alt="Carta" class="front" />
  <img src={coverSrc} alt="Carta sin revelar" class="back" />
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
  .card .front {
    position: absolute;
    transform: rotateY(90deg);
    transition: transform ease-in 0.2s;
  }
  .flipped .front {
    transform: rotateY(0deg);
    transition-delay: 0.2s;
  }
  .card .back {
    transition: transform ease-in 0.2s;
    transition-delay: 0.2s;
  }
  .flipped .back {
    transform: rotateY(90deg);
    transition-delay: 0s;
  }
</style>

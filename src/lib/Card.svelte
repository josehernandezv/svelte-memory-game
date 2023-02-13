<script>
  import coverSrc from "../assets/cover.png";

  export let src;
</script>

<div class="card">
  <img src={coverSrc} alt="Carta" />
</div>

<!-- <img {src} alt="Carta" /> -->
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

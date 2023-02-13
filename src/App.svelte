<script>
  import toadSrc from "./assets/toad.png";
  import flowerSrc from "./assets/flower.png";
  import tenCoinSrc from "./assets/10coins.png";
  import twentyCoinSrc from "./assets/20coins.png";
  import starSrc from "./assets/star.png";
  import oneUpSrc from "./assets/1up.png";
  import Card from "./lib/Card.svelte";

  let cardImages = [
    toadSrc,
    flowerSrc,
    tenCoinSrc,
    twentyCoinSrc,
    starSrc,
    oneUpSrc,
  ];
  let cards = [...cardImages, ...cardImages, ...cardImages];
</script>

<main>
  {#each cards as card}
    <Card src={card} />
  {/each}
</main>

<style>
  main {
    display: grid;
    grid-template-columns: repeat(6, 1fr);
    grid-gap: 1em;
  }
</style>

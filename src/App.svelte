<script>
  import toadSrc from "./assets/toad.png";
  import flowerSrc from "./assets/flower.png";
  import tenCoinSrc from "./assets/10coins.png";
  import twentyCoinSrc from "./assets/20coins.png";
  import starSrc from "./assets/star.png";
  import oneUpSrc from "./assets/1up.png";
  import Card from "./lib/Card.svelte";
  import { fade } from "svelte/transition";
  import { flip } from "svelte/animate";

  function shuffleCards() {
    let cardImages = [
      toadSrc,
      flowerSrc,
      tenCoinSrc,
      twentyCoinSrc,
      starSrc,
      oneUpSrc,
    ];
    let cards = [
      ...cardImages,
      ...cardImages,
      ...cardImages,
      ...cardImages,
    ].map((src, index) => ({
      src,
      id: index,
      solved: false,
    }));
    for (let i = cards.length - 1; i > 0; i--) {
      const j = Math.floor(Math.random() * (i + 1));
      [cards[i], cards[j]] = [cards[j], cards[i]];
    }
    return cards;
  }

  let cards = shuffleCards();
  let failures = 0;
  let choiceOne = null;
  let choiceTwo = null;

  function handleClick(card) {
    if (choiceOne && choiceTwo) {
      return;
    }
    if (choiceOne && choiceOne.id === card.id) {
      return;
    }
    if (choiceOne) {
      choiceTwo = card;
      if (choiceOne.src === choiceTwo.src) {
        cards = cards.map((c) => {
          if (c.id === choiceOne.id || c.id === choiceTwo.id) {
            return { ...c, solved: true };
          }
          return c;
        });
        choiceOne = null;
        choiceTwo = null;
      } else {
        setTimeout(() => {
          failures += 1;
          choiceOne = null;
          choiceTwo = null;
        }, 1000);
      }
    } else {
      choiceOne = card;
    }
  }

  $: if (failures >= 2) {
    alert("You lost!");
    setTimeout(() => {
      cards = shuffleCards();
    }, 200);
    failures = 0;
  }

  $: if (cards.every((card) => card.solved)) {
    alert(`You won in ${failures} failures 🥳!`);
    setTimeout(() => {
      cards = shuffleCards();
    }, 200);
    failures = 0;
  }
</script>

<main>
  {#each cards as card, index (card.id)}
    <div transition:fade={{ duration: 500, delay: index * 100 }} animate:flip>
      <Card
        src={card.src}
        flipped={card.solved || choiceOne === card || choiceTwo === card}
        on:flip={() => handleClick(card)}
      />
    </div>
  {/each}
</main>

<style>
  main {
    display: grid;
    grid-template-columns: repeat(6, 1fr);
    grid-gap: 1em;
  }
</style>

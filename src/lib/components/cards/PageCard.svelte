<script lang="ts">
	export let title = "Card";
	export let description = "This is a card";
	export let index = 0;
	export let scrollY = 0;

	let topOffset = index * 5 * 16 + 200;

	let scale = 1;
	let translateY = 0;

	let card: HTMLElement;
	let cardHeight = 0; // Define card height

	function isNextCardAtTop() {
		if (card) {
			cardHeight = card.offsetHeight;
			const nextCardTop = (index + 1) * cardHeight;
			return scrollY >= nextCardTop;
		}
		return false;
	}

	function scaleCard(scrollY: number, cardAtTop: boolean) {
		if (cardAtTop) {
			const shrinkStart = (index + 1) * cardHeight;
			const scrollPastStart = Math.max(0, scrollY - shrinkStart);
			scale = Math.max(0, 1 - scrollPastStart / 5000);
		} else {
			scale = 1;
		}
	}

	$: scaleCard(scrollY, isNextCardAtTop());

	const randomSeed = Math.floor(Math.random() * 100) + 1;
	const image = `https://picsum.photos/seed/${randomSeed}/1920/1080`;
</script>

<div
	style="
  top: {topOffset}px; 
  background-image: 
      linear-gradient(
        to bottom left in oklab, 
        oklch(60% .02 {index * 20 + 180}) 0%, oklch(90% .2 {index * 20 + 180}) 100%
      )
    ;
  transform:  translate3d(0, {translateY}px, 0) scale3d({scale}, {scale}, 1);
  filter: blur({scale * 0.5}px);
  "
	bind:this={card}
	class="card"
>
	<h2>{title}</h2>
	<p>{description}</p>
	<div class="img-container">
		<img src={image} alt="" />
	</div>
</div>

<style>
	.card {
		border-radius: 1rem;
		box-shadow: 0rem -0.5rem 2rem rgba(0, 0, 0, 0.2);
		border: 1px solid rgba(0, 0, 0, 0.1);
		padding: 1rem;

		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		max-width: 640px;

		position: sticky;
	}

	h2 {
		margin: 0;
		font-size: 5rem;
	}

	p {
		margin: 0;
		font-size: 2rem;
	}

	.img-container {
		width: 100%;
		border-radius: 1rem;
		overflow: hidden;
	}

	img {
		width: 100%;
		max-width: 100%;
		height: auto;
	}
</style>

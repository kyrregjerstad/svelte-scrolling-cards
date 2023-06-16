<script lang="ts">
	import PageCard from "$lib/components/cards/PageCard.svelte";

	let scrollY = 0;
</script>

<svelte:window bind:scrollY />

<section class="before">
	<h1>Scrolling cards</h1>
</section>

<div class="cards" style="transform: translate3d(0,{scrollY / -10}px, 0);">
	{#each Array(20) as _, i}
		<PageCard title={`Card ${i}`} description={`This is card ${i}`} index={i} {scrollY} />
	{/each}
	<div class="end" />
</div>

<section class="before">
	<h2>That's it :)</h2>
</section>

<style>
	h1,
	h2 {
		font-size: 10vw;
		color: white;
	}
	.before {
		display: flex;
		justify-content: center;
		align-items: center;
		height: 100vh;
		height: 100dvh;
		width: 100%;

		margin-bottom: 10rem;
	}
	.cards {
		position: relative;
		display: flex;
		flex-direction: column;
		align-items: center;

		gap: 3rem;
	}

	.end {
		height: 5rem;
		width: 100%;
	}
</style>

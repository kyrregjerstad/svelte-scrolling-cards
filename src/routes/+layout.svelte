<script lang="ts">
	import * as config from "$config";
	import { initLenis } from "$scripts/utils/initLenis";
	import "$styles/app.postcss";
	import { onMount } from "svelte";

	onMount(() => {
		initLenis();
	});
</script>

<svelte:head>
	<title>{config.title}</title>
</svelte:head>

<main>
	<slot />
</main>

<style lang="postcss">
	main {
		background-image: radial-gradient(
			farthest-corner circle at 103% 1% in oklch,
			oklch(80% 0.1 35) 0% 13%,
			oklch(66% 0.1 180) 100%
		);
	}
</style>

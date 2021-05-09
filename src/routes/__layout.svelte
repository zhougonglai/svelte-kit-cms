<script>
	import { page, navigating } from '$app/stores';
	import Nav from '$lib/Nav.svelte';
	import Footer from '$lib/Footer.svelte';
	import PreloadingIndicator from '$lib/PreloadingIndicator.svelte';
	import '../app.css';

	$: section = $page.path.split('/')[1];
</script>

<Nav {section} />

{#if $navigating}
	<PreloadingIndicator />
{/if}

<main>
	<slot />
</main>

<Footer />

<style lang="scss">
	main {
		min-height: calc(100vh - 100px - 345px);
	}
</style>

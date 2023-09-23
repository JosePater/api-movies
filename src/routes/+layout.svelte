<script>
	/** @type {import('./$types').LayoutData} */
	import Header from './Header.svelte';
	// export let data;
</script>

<div class="app">
	<Header />

	<main>
		<slot />
	</main>

	<footer />
</div>

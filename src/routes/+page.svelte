<script>
	/** @type {import('./$types').LayoutData} */
	export let data;
	import Loader from '../Components/Loader.svelte';
	import Grid from '../Components/Grid.svelte';
	const apiKey = data.key;

	let promesa = ajax();
	let peliculas = [];
	let numPage = 1;

	async function ajax(pag) {
		let url = `https://api.themoviedb.org/3/movie/popular?api_key=${apiKey}&language=en-US&page=${pag}`;
		const res = await fetch(url);
		peliculas = await res.json();

		if (res.ok) {
			return peliculas.results;
		} else {
			throw new Error('No hay conexión con la API');
		}
	}

	// Aumentar el número de páginas
	function nextPage() {
		numPage += 1;
		promesa = ajax(numPage);
	}

	// Disminuir el número de páginas
	function beforePage(num) {
		if (num === 1) {
			alert('Esta es la página # 1');
		} else {
			numPage -= 1;
			promesa = ajax(numPage);
		}
	}
</script>

<section class="container">
	<h1>Películas más populares</h1>

	{#await promesa}
		<div class="container"><Loader /></div>
	{:then peliculas}
		<Grid {peliculas} />

		<button
			id="btnLH"
			class="btn btn-warning position-fixed bottom-0 start-0 m-3"
			on:click={beforePage(numPage)}
		>
			<b>Página {numPage}.</b> ◀Ir atrás
		</button>

		<button id="btnRH" class="btn btn-warning position-fixed bottom-0 end-0 m-3" on:click={nextPage}
			>Ir a pág {numPage + 1} ▶
		</button>
	{:catch error}
		<p style="color:red">{error}</p>
	{/await}
</section>

<style>
	#btnLH,
	#btnRH {
		z-index: 999;
	}
</style>

<script>
	/** @type {import('./$types').LayoutData} */
	export let data;
	import Loader from '../Components/Loader.svelte';
	import GridCard from '../Components/GridCard.svelte';
	const apiKey = data.key;

	let promesa = ajax();
	let peliculas = [];
	let numPage = 1;
	let click = true; // input select 
	$: movieList = 'popular';
	let descrip = 'más populares';

	function opc() { // clic input select
		movieList == 'popular' ? (descrip = 'más populares') : null;
		movieList == 'now_playing' ? (descrip = 'en cartelera') : null;
		movieList == 'top_rated' ? (descrip = 'más valoradas') : null;
		movieList == 'upcoming' ? (descrip = 'próximamente') : null;
		// Avoid double updating when clicking
		click == true ? (click = false) : (click = true);
		if (click) {
			numPage = 1;
			promesa = ajax(numPage, movieList);
		}
	}

	async function ajax(pag, list = 'popular') {
		let url = `https://api.themoviedb.org/3/movie/${list}?api_key=${apiKey}&language=es-US&page=${pag}`;
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
		promesa = ajax(numPage, movieList);
	}

	// Disminuir el número de páginas
	function beforePage(num) {
		if (num === 1) {
			alert('Esta es la página # 1');
		} else {
			numPage -= 1;
			promesa = ajax(numPage, movieList);
		}
	}
</script>

<section class="container">
	<h1>Películas {descrip}</h1>
	<div class="col-2 mb-2 size-screen">
		<label for="">Listas de Películas</label>
		<select bind:value={movieList} on:click={opc} class="form-select">
			<option value="popular">Popular</option>
			<option value="now_playing">Now playing</option>
			<option value="top_rated">Top rated</option>
			<option value="upcoming">Upcoming</option>
		</select>
	</div>

	{#await promesa}
		<div class="container"><Loader /></div>
	{:then peliculas}
		<GridCard {peliculas} />
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
	@media screen and (max-width: 800px) {
		.size-screen {
			display: block;
			width: fit-content;
		}
	}
</style>

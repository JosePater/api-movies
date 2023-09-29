<script>
	/** @type {import('./$types').LayoutData} */
	export let data;
	import Loader from '../Components/Loader.svelte';
	import GridCard from '../Components/GridCard.svelte';
	const apiKey = data.key;

	const urlMain = `https://api.themoviedb.org/3/`;
	let searchedMovie = '';

	let promesa = ajax();
	let peliculas = [];
	let numPage = 1;
	let click = true; // input select
	$: movieList = 'popular';
	let descrip = 'más populares';

	function opc() {
		searchedMovie = '';
		// clic input select
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

	async function ajax(pag = 1, name = 'popular') {
		let url;
		if (searchedMovie == '') {
			url = `${urlMain}/movie/${name}?api_key=${apiKey}&language=es-US&page=${pag}`;
		} else {
			url = `${urlMain}/search/movie?query=${searchedMovie}&include_adult=false&language=es-US&page=${pag}&api_key=${apiKey}`;
		}
		const res = await fetch(url);
		peliculas = await res.json();

		if (res.ok) {
			return peliculas.results;
		} else {
			throw new Error('No hay conexión con la API');
		}
	}

	function search() {
		numPage = 1;
		searchedMovie.trim() != '' ? (promesa = ajax(numPage, searchedMovie)) : null;
	}

	// Aumentar el número de páginas
	function nextPage(peliculas) {
		if (peliculas[0] != undefined) {
			numPage += 1;
			promesa = ajax(numPage, movieList);
		} else {
			alert('No hay más película!');
		}
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
	<div class="row">
		<div class="col-3 size-screen">
			<label for="movie">Listas de películas</label>
			<select bind:value={movieList} on:click={opc} class="form-select mt-2">
				<option value="popular">Popular</option>
				<option value="now_playing">Now playing</option>
				<option value="top_rated">Top rated</option>
				<option value="upcoming">Upcoming</option>
			</select>
		</div>

		<div class="col">
			<form>
				<input
					type="text"
					class="form-control"
					bind:value={searchedMovie}
					placeholder="Buscar películas"
					required
				/>
				<button type="submit" class="btn btn-primary" on:click={search}>Buscar</button>
			</form>
		</div>
	</div>

	{#await promesa}
		<div class="container"><Loader /></div>
	{:then peliculas}
		<GridCard {peliculas} {numPage} />
		<button
			id="btnLH"
			class="btn btn-warning position-fixed bottom-0 start-0 m-3"
			on:click={beforePage(numPage)}
		>
			<b>Página {numPage}.</b> ◀Ir atrás
		</button>

		<button
			id="btnRH"
			class="btn btn-warning position-fixed bottom-0 end-0 m-3"
			on:click={nextPage(peliculas)}
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
	.row {
		align-items: center;
	}
	form {
		display: flex;
		flex-direction: row;
		align-content: center;
		justify-content: center;
		align-items: center;
	}
	form input {
		margin: auto;
		margin-right: 15px;
		border-color: rgb(96, 248, 142);
		padding: 8px;
		width: 80%;
	}
	@media screen and (max-width: 800px) {
		.size-screen {
			display: block;
			width: fit-content;
		}
		form input {
			width: 100%;
		}
	}
	@media screen and (max-width: 410px) {
		form input,
		form button {
			display: block;
			margin: 5px;
			width: fit-content;
		}
		.col-3 {
			margin: auto;
			/* width: fit-content; */
			margin-bottom: 5px;
		}
	}
</style>

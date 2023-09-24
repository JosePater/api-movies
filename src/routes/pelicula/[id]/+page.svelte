<script>
	import { page } from '$app/stores';
	let { id } = $page.params; // Recibe el parámetro

	const url = 'https://api.themoviedb.org/3/movie/';
	const key = '?api_key=06aca6f9ab6fc84ea9c50869f995ed68&language=en-US';
	const urlFinal = url + id + key;

	let promesa = ajax();
	let pelicula = {};
	let generos = [];

	async function ajax() {
		const res = await fetch(urlFinal);
		pelicula = await res.json();
		generos = await pelicula.genres;
		if (res.ok) {
			return pelicula.results;
		} else {
			throw new Error('Hubo un error');
		}
	}
</script>

<div class="row mt-5">
	<div class="col-lg-6">
		<img
			src="https://image.tmdb.org/t/p/w500{pelicula.poster_path}"
			alt={pelicula.title}
			width="100%"
			height="700"
		/>
	</div>

	<div class="col-lg-6">
		<h1>{pelicula.title}</h1>
		<p>{pelicula.overview}</p>
		{#each generos as genero}
			<h4>{genero.name}</h4>
		{/each}

		<div class="rating" align="center">
			{pelicula.vote_average}
		</div>
	</div>
</div>

<style>
	.rating {
		width: 300px;
		border: solid 4px black;
		font-size: 5rem;
		font-weight: bolder;
	}
</style>

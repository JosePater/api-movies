<script>
	/** @type {import('./$types').LayoutData} */
	export let data;
	import Loader from '../../../Components/Loader.svelte';
	import { onMount } from 'svelte';
	import { page } from '$app/stores'; // Need for receive param

	let { id } = $page.params; // Recibe el parámetro
	const apiKey = data.key;
	let urlMain = `https://api.themoviedb.org/3/`;

	let pelicula = {};
	let generos = [];
	let error;

	onMount(async () => {
		const url = `${urlMain}movie/${id}?api_key=${apiKey}&language=es-US`;

		try {
			const res = await fetch(url);

			if (res.ok) {
				pelicula = await res.json();
				generos = pelicula.genres;
			} else {
				throw new Error('Película no encontrada');
			}
		} catch (e) {
			error = e.message;
		}
	});
</script>

<section class="container">
	{#if pelicula.title}
		<div class="row mt-5">
			<div class="col-lg-6">
				<img
					src="https://image.tmdb.org/t/p/w500{pelicula.poster_path}"
					alt={pelicula.title}
					width="100%"
					height="600"
				/>
			</div>

			<div class="col-lg-6">
				<h1>{pelicula.title}</h1>
				<p>{pelicula.overview}</p>
				{#each generos as genero}
					<h4>{genero.name}</h4>
				{/each}

				<p><b>Duración:</b> {pelicula.runtime} min</p>

				<div class="rating" align="center">
					{pelicula.vote_average}
				</div>
			</div>

			{#if pelicula.backdrop_path != null}
				<img
					src="https://image.tmdb.org/t/p/w500{pelicula.backdrop_path}"
					alt={pelicula.title}
					class="mt-3 mb-2"
					width="100%"
					height="100%"
				/>
			{/if}
		</div>
	{:else if error}
		<p id="error">🚫{error}</p>
	{:else}
		<div class="container"><Loader /></div>
	{/if}
</section>

<style>
	.rating {
		width: 300px;
		border: solid 4px black;
		font-size: 5rem;
		font-weight: bolder;
	}
	#error {
		color: red;
		font-size: 28px;
	}
</style>

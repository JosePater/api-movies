<script>
	/** @type {import('./$types').LayoutData} */
	export let data;
	import Loader from '../Components/Loader.svelte';
    import Grid from '../Components/Grid.svelte';
	import { page } from '$app/stores'; // Need for receive param
	let { id } = $page.params; // Recibe el parámetro
	const apiKey = data.key;

	let url =
	`https://api.themoviedb.org/3/movie/popular?api_key=${apiKey}&language=en-US&page=1`;

	let promesa = ajax();
	let peliculas = [];

	async function ajax() {
		const res = await fetch(url);
		peliculas = await res.json();

		if (res.ok) {
			return peliculas.results;
		} else {
			throw new Error('No hay conexión con la API');
		}
	}
</script>

<section class="container">
	<h1>Películas más populares</h1>

	{#await promesa}
		<div class="container"><Loader /></div>
	{:then peliculas}
		<Grid {peliculas}/>
	{:catch error}
		<p style="color:red">{error}</p>
	{/await}
</section>

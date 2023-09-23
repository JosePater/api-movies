<script>
	import Loader from '../Components/Loader.svelte';
    import Grid from '../Components/Grid.svelte';
	let url =
		'https://api.themoviedb.org/3/movie/popular?api_key=06aca6f9ab6fc84ea9c50869f995ed68&language=en-US&page=1';

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

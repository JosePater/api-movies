<script>
	import Card from './Card.svelte';
	import { goto } from '$app/navigation';
	export let peliculas;
</script>

<div class="row mt-3">
	{#each peliculas as item}
		<div class="col-sm-4">
			<Card
				titulo={item.title}
				imagen={item.poster_path}
				fecha={item.release_date}
				on:ver-mas={() => goto(`/pelicula/${item.id}`)}
			/>
		</div>
	{/each}
</div>
<script>
	import { goto } from '$app/navigation';
	export let peliculas;
	export let numPage;
</script>

<div class="row mt-3">
	{#if peliculas[0] == undefined}
		<h2>{numPage == 1 ? 'Película no encontrada' : 'No hay más películas'}❗</h2>
	{/if}

	{#each peliculas as item}
		{#if item.poster_path != null}
			<div class="col-sm-3 size-screen">
				<div class="card mb-3 size-screen">
					<img src={`https://image.tmdb.org/t/p/w400${item.poster_path}`} alt={item.title} />
					<div class="card-body">
						<h5 class="card-title">{item.title}</h5>
						<h6 class="card-title">Fecha de lanzamiento: {item.release_date}</h6>
						<button class="btn btn-primary" on:click={() => goto(`/pelicula/${item.id}`)}
							>Ver más</button
						>
					</div>
				</div>
			</div>
		{/if}
	{/each}
</div>

<style>
	.card {
		background-color: rgb(199, 243, 247);
	}
	@media screen and (max-width: 770px) {
		.size-screen {
			margin: auto;
			padding: 2px;
			display: block;
			width: min-content;
			align-items: center;
		}
	}
</style>

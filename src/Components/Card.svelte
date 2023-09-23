<script>
	export let titulo;
	export let imagen;
	export let fecha;
	import { createEventDispatcher } from 'svelte';
	const dispatch = createEventDispatcher();

	function ver() {
		dispatch('ver-mas');
	}
</script>

<div class="card mb-3" style="width: 18rem;">
	<img src={`https://image.tmdb.org/t/p/w500${imagen}`} alt={titulo} width="100%" height="500" />
	<div class="card-body">
		<h5 class="card-title">{titulo}</h5>
		<h6 class="card-title">Fecha de lanzamiento: {fecha}</h6>
		<button class="btn btn-primary" on:click={ver}>Ver más</button>
	</div>
</div>

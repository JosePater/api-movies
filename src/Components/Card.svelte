<script>
	export let titulo;
	export let imagen;
</script>

<div class="card mb-3" style="width: 18res;">
	<img src="https://image.tmdb.org/t/p/w500{imagen}" alt={titulo} width="100%" height="500" />
	<div class="card-body">
		<h5 class="card-title">{titulo}</h5>
	</div>
</div>

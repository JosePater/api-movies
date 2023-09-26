<!-- AcercaDe.svelte -->

<script>
	// Puedes agregar cualquier lógica necesaria aquí
</script>

<main>
	<h1>Acerca de</h1>

	<p>
		Este proyecto es una aplicación web que utiliza la API de The Movie Database (TMDb) para mostrar
		información sobre películas.
	</p>

	<p>Está basado en un proyecto desarrollado por el ingeniero Jorge Maldonado B. (tutor Udemy).</p>

	<h2>Nuevas Funcionalidades</h2>
	<ul>
		<li>Adaptado a SvelteKit.</li>
		<li>
			Filtra películas por categorías como popularidad, calificación, en cartelera y próximamente.
		</li>
		<li>Busca más películas mediante botones (Retroceder y Avanzar).</li>
		<li>Renderiza el cargador (CSS) mientras se visualiza la película seleccionada.</li>
		<li>Se adapta a dispositivos pequeños (responsive).</li>
		<li>Contiene la apiKey del lado del servidor.</li>
	</ul>

	<h2>Tecnologías Utilizadas</h2>
	<div class="container mb-5">
		<a
			href="https://developer.mozilla.org/en-US/docs/Web/HTML"
			target="_blank"
			rel="noopener noreferrer"
		>
			<img
				src="https://raw.githubusercontent.com/devicons/devicon/master/icons/html5/html5-original-wordmark.svg"
				alt="HTML5"
				width="40"
				height="40"
			/>
		</a>
		<a
			href="https://developer.mozilla.org/en-US/docs/Web/CSS"
			target="_blank"
			rel="noopener noreferrer"
		>
			<img
				src="https://raw.githubusercontent.com/devicons/devicon/master/icons/css3/css3-original-wordmark.svg"
				alt="CSS3"
				width="40"
				height="40"
			/>
		</a>
		<a
			href="https://developer.mozilla.org/en-US/docs/Web/JavaScript"
			target="_blank"
			rel="noopener noreferrer"
		>
			<img
				src="https://raw.githubusercontent.com/devicons/devicon/master/icons/javascript/javascript-original.svg"
				alt="JavaScript"
				width="40"
				height="40"
			/>
		</a>
		<a href="https://getbootstrap.com" target="_blank" rel="noopener noreferrer">
			<img
				src="https://raw.githubusercontent.com/devicons/devicon/master/icons/bootstrap/bootstrap-plain-wordmark.svg"
				alt="Bootstrap"
				width="40"
				height="40"
			/>
		</a>
		<a href="https://svelte.dev" target="_blank" rel="noopener noreferrer">
			<img
				src="https://raw.githubusercontent.com/devicons/devicon/master/icons/svelte/svelte-original-wordmark.svg"
				alt="Svelte"
				width="40"
				height="40"
			/>
		</a>
	</div>

	<h2>Desarrollado por</h2>
	<p><strong>[José Luis Paternina Martínez]</strong></p>
</main>


<style>
	main {
		font-family: Arial, sans-serif;
		max-width: 800px;
		margin: 0 auto;
    margin-top: 30px;
		padding: 20px;
		background-color: #fcedbd;
		border: 1px solid #ccc;
		border-radius: 8px;
		box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
	}

	.container {
		display: flex;
		gap: 20px;
		margin-top: 10px;
	}

	.container img:hover {
		transform: scale(1.2);
	}
</style>

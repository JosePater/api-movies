<script>
    import Card from './Card.svelte';
    export let peliculas
    import { goto } from '$app/navigation';
</script>

<div class="row mt-3">
{#each peliculas as item}
    <div class="col-sm-4">
        <!-- Componente Card -->
        <Card
        titulo={item.title}
        imagen={item.poster_path}
        fecha={item.release_date}
        on:ver-mas={() => goto(`/Pelicula/${item.id}`)}
        />
    </div>
{/each}
</div>
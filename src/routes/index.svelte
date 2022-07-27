<script context="module">
    export async function load({}){
        const url = 'https://pokeapi.co/api/v2/pokemon?limit=150'
        const res = await fetch(url)
        const data = await res.json()
        const loadedPokemon = data.results.map((data, index) => {
            return {
                name: data.name,
                id: index + 1,
                image: `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${index + 1}.png`
            }
        })
        return {props: {loadedPokemon: loadedPokemon}}
    }
</script>

<script>
    export let loadedPokemon
    console.log(loadedPokemon)
    import {pokemon} from '$lib/stores/pokestore'
    import {onMount} from 'svelte'
    import PokemanCard from './components/pokemanCard.svelte'
    pokemon.update((n) => n = loadedPokemon)
    
    let searchTerm = ''
    let filteredPokemon = []

    $: {
        console.log(searchTerm)
        if (searchTerm) {
            filteredPokemon = $pokemon.filter( pokeman => pokeman.name.toLowerCase().includes(searchTerm.toLowerCase()))
        } else {
            filteredPokemon = [...$pokemon]
        }
    }

    
</script>

<svelte:head>
    <title>Pokedex</title>    
</svelte:head>

<h1 class='text-4xl text-center my-8 uppercase'>Home</h1>

<input type="text" class='w-full rounded-md text-lg p-4 border-2 border-gray-200' placeholder="Search Pokemon" bind:value={searchTerm}>

<div class="py-4 grid gap-4 md:grid-cols-2 grid-cols-1">
    {#if $pokemon}
    {#each filteredPokemon as pokeman}
    <PokemanCard {pokeman}/>
    {/each}
{/if}
</div>




<style>

</style>
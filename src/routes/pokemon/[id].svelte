<script context="module">
    export async function load({url, params}){
        const id = params.id
        const urls = `https://pokeapi.co/api/v2/pokemon/${id}`
        const res = await fetch(urls)
        const pokeman = await res.json()
        return {props: {pokeman}}
    }
</script>


<script>
    export let pokeman
    console.log(pokeman)
</script>

<div class="flex flex-col items-center">
    <h1 class='text-4xl text-center my-8 uppercase'>{pokeman.name}</h1>
    <p>Type: 
        {#each pokeman.types as pokeType, i}
        
            <strong><span>{pokeType.type.name}</span></strong> 
            {#if (i + 1) !== pokeman.types.length}
                <span class='mr-1'> &</span> 
            {/if}
        {/each}
        |
        Height: <strong><span>{pokeman.height}</span></strong>
        |
        Weight: <strong><span>{pokeman.weight}</span></strong>
    </p>
    <img class="card-image" src="{pokeman.sprites['front_default']}" alt="{pokeman.name}">
    
</div>


<style>

</style>
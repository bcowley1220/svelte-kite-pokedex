<script>
    export let pokeman
</script>

<!-- <p>{pokeman.name}</p> -->
<a href={`/pokemon/${pokeman.id}`} class="list-none p-6 bg-gray-100 text-gray-800 text-center rounded-md shadow-sm hover:shadow-md flex flex-col items-center">
    <img class="h-40 w-40" src="{pokeman.image}" alt="{pokeman.name}">
    <h2 class="uppercase text-xl">{pokeman.id}. {pokeman.name}</h2>
</a>
<style>

</style>
<script context="module">
  export async function load({page}){
    const url = "https://pokeapi.co/api/v2/pokemon?limit=150"
    const res = await fetch(url);
    const data = await res.json();
    const loadedPokemon = data.results.map((data, index) => {
        return {
            name: data.name,
            id: index + 1,
            image:`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${
                index + 1
            }.png`
        };
    });
    return {props: {pokemon:loadedPokemon}}
  }
</script>

<script>
    import PokemanCard from "../components/pokemanCard.svelte"
    export let pokemon;
    
    let searchTerm = "";
    let filterPokemon = [];

    $: {

        if(searchTerm){
          //search pokemon
          filterPokemon = pokemon.filter(pokeman => pokeman.name.toLowerCase().includes(searchTerm.toLowerCase()));
        }else {
          filterPokemon = [... pokemon]
        }
    }

</script>

<svelte:head>
    <title>SwelteKit Pokedex</title>
</svelte:head>

<h1 class="text-4xl text-center my-8 uppercase" >Svelte kit Pokedex</h1>
<input class="w-full rounded-md text-lg p-4 border-2 border-gray-200" type="text" bind:value={searchTerm} placeholder="Search Pokemon" > 
<div class="py-4 grid gap-4 md:grid-cols-2 grid-cols-1" >  
  {#each filterPokemon as pokeman}
    <PokemanCard pokeman={pokeman}/>
  {/each}
</div>
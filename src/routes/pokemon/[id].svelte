<script context="module">
    export async function load({page}){
        const id = page.params.id;
        const url = `https://pokeapi.co/api/v2/pokemon/${id}`;
        const res = await fetch(url);
        const pokeman = await res.json();
        return {props: {pokeman}}; 

    }
</script>

<script>
    export let pokeman;
    const type = pokeman.types[0].type.name;
    console.log(pokeman);
</script>

<style>
  .center {
  display: block;
  margin-left: auto;
  margin-right: auto;
  width: 50%;
}
</style>

<div class="flex flex-col text-center">
<h1 class="text-4xl text-center my-8 uppercase" >{pokeman.name}</h1>

<p>Type: <strong>{type}</strong> | Height: <strong>{pokeman.height}</strong>
    | Weight: <strong>{pokeman.weight}</strong>
</p>

<img class="card-image, center" styles width="200" src={pokeman.sprites['front_default']} alt={pokeman.name} />
</div>
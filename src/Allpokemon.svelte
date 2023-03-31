<script>
let pokemonList = [];
let searchValue = "";
let pokemonData = null;
const apiUrl = "https://pokeapi.co/api/v2/pokemon";
  
async function fetchPokemonList() {
	const response = await fetch(`${apiUrl}?limit=20`);
	const data = await response.json();
	pokemonList = data.results;
}
  
function searchPokemon() {
	fetch(`${apiUrl}/${searchValue}`)
	.then(response => response.json())
	.then(data => {
		pokemonData = {
		name: data.name,
		id: data.id,
		height: data.height,
		weight: data.weight,
		image: data.sprites.front_default
};
})
	.catch(error => console.error(error));
};
</script>

<main>
	<h1>Pokemon Search</h1>
	<input type="text" bind:value={searchValue} placeholder="Enter a Pokemon name" />
	<button on:click={searchPokemon}>Search</button>
  
	{#if pokemonData}
	<div>
		<h2>{pokemonData.name}</h2>
		<img src={pokemonData.image} alt={pokemonData.name} />
		<p>ID: {pokemonData.id}</p>
		<p>Height: {pokemonData.height}</p>
		<p>Weight: {pokemonData.weight}</p>
	</div>
	{:else}
	  <p>No Pokemon found</p>
	{/if}
</main>

<style>
*{
    margin: 10px;
}
div{
	position: fixed;
	margin-left: 20px;
    padding: 10px;
    border: 1px solid #ccc;
    margin-bottom: 10px;
}
</style>
  
  
  
<script>
	import { selectedPokemonStore } from '../module/selectedPokemonStore';
	let selectedContent = '';
	let ans = '';

	function onSubmit() {
		selectedPokemonStore.update((n) => {
			ans = selected.id;
			n = ans;
			return n;
		});
	}
	selectedPokemonStore.subscribe((value) => {
		selectedContent = value;
	});

	let pokemons = [];
	for (let i = 1; i <= 151; i++) {
		pokemons.push({ id: i, text: i });
	}
	let selected = '';
</script>

<select
	bind:value={selected}
	name="poke"
	on:change={() => {
		onSubmit();
	}}
	id=""
>
	{#each pokemons as pokemon}
		<option value={pokemon}>{pokemon.text}</option>
	{/each}
</select>
<p>{selectedContent}</p>

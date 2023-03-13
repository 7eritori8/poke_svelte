<!-- <script>
	async function getPokeInfo() {
		const res = await fetch('https://pokeapi.co/api/v2/pokemon/25');
		const resContent = await res.json();
		console.log({ resContent });
		if (res.ok) {
			return resContent;
		} else {
			throw new Error(resContent);
		}
	}
	let promise = getPokeInfo();
	function handleClick() {
		promise = getPokeInfo();
		console.log(promise.json());
	}
</script>

<button
	on:click={() => {
		handleClick();
	}}>eee</button
> -->
<script>
	import { selectedPokemonStore } from '../module/selectedPokemonStore';
	let selectedContent = '';

	selectedPokemonStore.subscribe((value) => {
		selectedContent = value;
	});
	async function getPokeInfo() {
		const res = await fetch(`https://pokeapi.co/api/v2/pokemon/${selectedContent}`);
		const text = await res.json();
		if (res.ok) {
			return text;
		} else {
			throw new Error(text);
		}
	}
	let promise = getPokeInfo();

	function handleClick() {
		promise = getPokeInfo();
	}
</script>

<div class="content">
	<button
		on:click={() => {
			handleClick();
		}}>ぴっぴかちゅう</button
	>
	{#await promise}
		<p class="load">Loading...</p>
	{:then answer}
		<h1>{answer.name}</h1>
		<img src={answer.sprites.front_default} alt="" />
	{/await}
</div>

<script>
	import * as Tone from 'tone';
	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

	export let isPowerOn = false;

	async function handleClick() {
		if (!isPowerOn) {
			await Tone.start();
			isPowerOn = true;
			dispatch('synth', {
				synth: new Tone.PolySynth(Tone.Synth).toDestination()
			});
		} else {
			isPowerOn = false;
		}
	}
</script>

<button on:click={handleClick}> Start audio </button>

{#if isPowerOn}
	<style>
		button {
			background-color: green;
		}
	</style>
{:else}
	<style>
		button {
			background-color: red;
		}
	</style>
{/if}

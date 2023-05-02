<script lang="ts">
	import * as Tone from 'tone';
	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

	export let isPowerOn = false;
	export let synthList: Tone.Synth[] = [];

	async function handleClick() {
		if (!isPowerOn) {
			await Tone.start();
			isPowerOn = true;

			for (let i = 0; i < 13; i++) {
				synthList.push(new Tone.Synth().toDestination());
			}

			console.log('dispatch synthList');

			dispatch('synthList', {
				synthList: synthList
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

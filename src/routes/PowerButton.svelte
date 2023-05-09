<script lang="ts">
	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

	let isPowerOn = false;

	async function handleClick() {
		isPowerOn ? (isPowerOn = false) : (isPowerOn = true);
		dispatch('togglePower', {
			isPowerOn: isPowerOn
		});
	}
</script>

<button id="powerButton" on:click={handleClick}> Start audio </button>

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

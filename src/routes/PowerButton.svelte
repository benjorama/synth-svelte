<script>
	import * as Tone from 'tone';

	export let isPowerOn = false;

	async function handleClick() {
		if (!isPowerOn) {
			await Tone.start();
			isPowerOn = true;
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

<script lang="ts">
	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

	function handleChange(e: Event) {
		const target: HTMLSelectElement = <HTMLSelectElement>e.target;
		dispatch('selectSynth', {
			value: target.value
		});
		let keyboard = document.getElementById('keyboard');
		keyboard ? keyboard.focus() : '';
	}
</script>

<label for="synth-selector">Choose a synth:</label>

<select on:change={handleChange} name="synths" id="synth-selector">
	<option value="default">Synth</option>
	<option value="amsynth">AMSynth</option>
	<option value="duosynth">DuoSynth</option>
	<option value="membranesynth">MembraneSynth</option>
	<option value="metalsynth">MetalSynth</option>
	<option value="monosynth">MonoSynth</option>
	<option value="noisesynth">NoiseSynth</option>
	<option value="plucksynth">PluckSynth</option>
</select>

<style>
</style>

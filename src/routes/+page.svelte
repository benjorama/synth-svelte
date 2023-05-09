<script lang="ts">
	import * as Tone from 'tone';
	import Keyboard from './Keyboard.svelte';
	import PowerButton from './PowerButton.svelte';
	import SelectSynth from './SelectSynth.svelte';

	let isPowerOn = false;
	let selectedSynth: Tone.Synth[] = [];

	async function handleTogglePower(e: { detail: { isPowerOn: boolean } }) {
		isPowerOn = e.detail.isPowerOn;
		if (isPowerOn) {
			await Tone.start();
			initSynth();
		} else {
			selectedSynth.forEach((synth) => {
				synth.dispose();
				selectedSynth = [];
			});
			isPowerOn = false;
		}
	}

	function initSynth() {
		for (let i = 0; i < 13; i++)
			selectedSynth = [...selectedSynth, new Tone.Synth().toDestination()];

		let Keyboard = document.getElementById('keyboard');
		Keyboard?.focus();
	}
</script>

<h1>Synth</h1>
<PowerButton on:togglePower={handleTogglePower} />
<SelectSynth />
<Keyboard {selectedSynth} />

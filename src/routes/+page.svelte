<script lang="ts">
	import * as Tone from 'tone';
	import Keyboard from './Keyboard.svelte';
	import PowerButton from './PowerButton.svelte';
	import SelectSynth from './SelectSynth.svelte';

	let isPowerOn = false;
	let selectedSynth = 'default';
	let loadedSynth: Tone.Synth[] = [];

	async function handleTogglePower(e: { detail: { isPowerOn: boolean } }) {
		isPowerOn = e.detail.isPowerOn;
		if (isPowerOn) {
			await Tone.start();
			initSynth();
		} else {
			loadedSynth.forEach((synth) => {
				synth.dispose();
				loadedSynth = [];
			});
			isPowerOn = false;
		}
	}

	function handleSelectSynth(e: { detail: { value: string } }) {
		selectedSynth = e.detail.value;
	}

	function initSynth() {
		for (let i = 0; i < 13; i++) loadedSynth = [...loadedSynth, new Tone.Synth().toDestination()];

		let Keyboard = document.getElementById('keyboard');
		Keyboard?.focus();
	}
</script>

<h1>Synth</h1>
<PowerButton on:togglePower={handleTogglePower} />
<SelectSynth on:selectSynth={handleSelectSynth} />
<Keyboard {loadedSynth} />

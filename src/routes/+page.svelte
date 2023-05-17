<script lang="ts">
	import * as Tone from 'tone';
	import Keyboard from './Keyboard.svelte';
	import PowerButton from './PowerButton.svelte';
	import SelectSynth from './SelectSynth.svelte';

	let isPowerOn = false;
	let selectedSynth = 'default';
	let loadedSynth: (
		| Tone.Synth
		| Tone.AMSynth
		| Tone.DuoSynth
		| Tone.MembraneSynth
		| Tone.MetalSynth
		| Tone.MonoSynth
		| Tone.NoiseSynth
		| Tone.PluckSynth
	)[] = [];

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
		loadedSynth.forEach((synth) => {
			synth.dispose();
			loadedSynth = [];
		});
		initSynth();
	}

	function initSynth() {
		switch (selectedSynth) {
			case 'default':
				for (let i = 0; i < 13; i++)
					loadedSynth = [...loadedSynth, new Tone.Synth().toDestination()];
				break;
			case 'amsynth':
				for (let i = 0; i < 13; i++)
					loadedSynth = [...loadedSynth, new Tone.AMSynth().toDestination()];
				break;
			case 'duosynth':
				for (let i = 0; i < 13; i++)
					loadedSynth = [...loadedSynth, new Tone.DuoSynth().toDestination()];
				break;
			case 'membranesynth':
				for (let i = 0; i < 13; i++)
					loadedSynth = [...loadedSynth, new Tone.MembraneSynth().toDestination()];
				break;
			case 'metalsynth':
				for (let i = 0; i < 13; i++)
					loadedSynth = [...loadedSynth, new Tone.MetalSynth().toDestination()];
				break;
			case 'monosynth':
				for (let i = 0; i < 13; i++)
					loadedSynth = [...loadedSynth, new Tone.MonoSynth().toDestination()];
				break;
			case 'noisesynth':
				for (let i = 0; i < 13; i++)
					loadedSynth = [...loadedSynth, new Tone.NoiseSynth().toDestination()];
				break;
			case 'plucksynth':
				for (let i = 0; i < 13; i++)
					loadedSynth = [...loadedSynth, new Tone.PluckSynth().toDestination()];
				break;
			default:
		}

		let Keyboard = document.getElementById('keyboard');
		Keyboard?.focus();
	}
</script>

<h1>Synth</h1>
<PowerButton on:togglePower={handleTogglePower} />
<SelectSynth on:selectSynth={handleSelectSynth} />
<Keyboard {loadedSynth} />

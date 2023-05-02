<script lang="ts">
	import type * as Tone from 'tone';
	import PowerButton from './PowerButton.svelte';
	import Key from './Key.svelte';

	export let synth: Tone.Synth | undefined = undefined;

	function handleSaveSynth(e: { detail: { synth: Tone.Synth<Tone.SynthOptions> } }) {
		synth = e.detail.synth;
	}
</script>

<div>
	<PowerButton on:synth={handleSaveSynth} />
	<div class="whiteKeys">
		<Key pitch={'C4'} {synth} />
		<Key pitch={'D4'} {synth} />
		<Key pitch={'E4'} {synth} />
		<Key pitch={'F4'} {synth} />
		<Key pitch={'G4'} {synth} />
		<Key pitch={'A4'} {synth} />
		<Key pitch={'B4'} {synth} />
		<Key pitch={'C5'} {synth} />
	</div>

	<div class="blackKeys">
		<div class="group2">
			<Key pitch={'C#4'} {synth} />
			<Key pitch={'D#4'} {synth} />
		</div>
		<div class="group3">
			<Key pitch={'F#4'} {synth} />
			<Key pitch={'G#4'} {synth} />
			<Key pitch={'A#4'} {synth} />
		</div>
	</div>
</div>

<style>
	.whiteKeys {
		display: flex;
		justify-content: center;
	}

	.blackKeys {
		display: flex;
		position: relative;
		bottom: 14em;
		right: 0.5em;
		justify-content: center;
	}

	.group2 {
		display: flex;
		position: relative;
		right: 3em;
	}
	.group3 {
		display: flex;
	}
</style>

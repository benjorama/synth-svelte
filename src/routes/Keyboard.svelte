<script lang="ts">
	import type * as Tone from 'tone';
	import PowerButton from './PowerButton.svelte';
	import Key from './Key.svelte';

	export let synthList: Tone.Synth[] | undefined = undefined;

	function handleSaveSynth(e: { detail: { synthList: Tone.Synth<Tone.SynthOptions>[] } }) {
		synthList = e.detail.synthList;
		console.log('synth saved');
	}

	function handleKeyDown(e: KeyboardEvent) {
		console.log('key down: ' + e.key);
		if (synthList) {
			e.key === 'a' ? synthList[0]?.triggerAttack('C4') : '';
			e.key === 's' ? synthList[1]?.triggerAttack('D4') : '';
			e.key === 'd' ? synthList[2]?.triggerAttack('E4') : '';
			e.key === 'f' ? synthList[3]?.triggerAttack('F4') : '';
			e.key === 'j' ? synthList[4]?.triggerAttack('G4') : '';
			e.key === 'k' ? synthList[5]?.triggerAttack('A4') : '';
			e.key === 'l' ? synthList[6]?.triggerAttack('B4') : '';
			e.key === ';' ? synthList[7]?.triggerAttack('C5') : '';
			e.key === 'w' ? synthList[8]?.triggerAttack('C#4') : '';
			e.key === 'e' ? synthList[9]?.triggerAttack('D#4') : '';
			e.key === 'u' ? synthList[10]?.triggerAttack('F#4') : '';
			e.key === 'i' ? synthList[11]?.triggerAttack('G#4') : '';
			e.key === 'o' ? synthList[12]?.triggerAttack('A#4') : '';
		}
	}

	function handleKeyUp(e: KeyboardEvent) {
		console.log('key up: ' + e.key);
		if (synthList) {
			e.key === 'a' ? synthList[0]?.triggerRelease() : '';
			e.key === 's' ? synthList[1]?.triggerRelease() : '';
			e.key === 'd' ? synthList[2]?.triggerRelease() : '';
			e.key === 'f' ? synthList[3]?.triggerRelease() : '';
			e.key === 'j' ? synthList[4]?.triggerRelease() : '';
			e.key === 'k' ? synthList[5]?.triggerRelease() : '';
			e.key === 'l' ? synthList[6]?.triggerRelease() : '';
			e.key === ';' ? synthList[7]?.triggerRelease() : '';
			e.key === 'w' ? synthList[8]?.triggerRelease() : '';
			e.key === 'e' ? synthList[9]?.triggerRelease() : '';
			e.key === 'u' ? synthList[10]?.triggerRelease() : '';
			e.key === 'i' ? synthList[11]?.triggerRelease() : '';
			e.key === 'o' ? synthList[12]?.triggerRelease() : '';
		}
	}
</script>

<div on:keydown={handleKeyDown} on:keyup={handleKeyUp}>
	<PowerButton on:synthList={handleSaveSynth} />
	<div class="whiteKeys">
		<Key pitch={'C4'} synth={synthList ? synthList[0] : undefined} />
		<Key pitch={'D4'} synth={synthList ? synthList[1] : undefined} />
		<Key pitch={'E4'} synth={synthList ? synthList[2] : undefined} />
		<Key pitch={'F4'} synth={synthList ? synthList[3] : undefined} />
		<Key pitch={'G4'} synth={synthList ? synthList[4] : undefined} />
		<Key pitch={'A4'} synth={synthList ? synthList[5] : undefined} />
		<Key pitch={'B4'} synth={synthList ? synthList[6] : undefined} />
		<Key pitch={'C5'} synth={synthList ? synthList[7] : undefined} />
	</div>

	<div class="blackKeys">
		<div class="group2">
			<Key pitch={'C#4'} synth={synthList ? synthList[8] : undefined} />
			<Key pitch={'D#4'} synth={synthList ? synthList[9] : undefined} />
		</div>
		<div class="group3">
			<Key pitch={'F#4'} synth={synthList ? synthList[10] : undefined} />
			<Key pitch={'G#4'} synth={synthList ? synthList[11] : undefined} />
			<Key pitch={'A#4'} synth={synthList ? synthList[12] : undefined} />
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

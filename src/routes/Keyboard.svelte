<script lang="ts">
	import type * as Tone from 'tone';
	import Key from './Key.svelte';

	export let selectedSynth: Tone.Synth[];

	let keysDown: string[] = [];

	function handleKeyDown(e: KeyboardEvent) {
		if (selectedSynth && !keysDown.includes(e.key)) {
			e.key === 'a' ? selectedSynth[0]?.triggerAttack('C4') : '';
			e.key === 's' ? selectedSynth[1]?.triggerAttack('D4') : '';
			e.key === 'd' ? selectedSynth[2]?.triggerAttack('E4') : '';
			e.key === 'f' ? selectedSynth[3]?.triggerAttack('F4') : '';
			e.key === 'j' ? selectedSynth[4]?.triggerAttack('G4') : '';
			e.key === 'k' ? selectedSynth[5]?.triggerAttack('A4') : '';
			e.key === 'l' ? selectedSynth[6]?.triggerAttack('B4') : '';
			e.key === ';' ? selectedSynth[7]?.triggerAttack('C5') : '';
			e.key === 'w' ? selectedSynth[8]?.triggerAttack('C#4') : '';
			e.key === 'e' ? selectedSynth[9]?.triggerAttack('D#4') : '';
			e.key === 'u' ? selectedSynth[10]?.triggerAttack('F#4') : '';
			e.key === 'i' ? selectedSynth[11]?.triggerAttack('G#4') : '';
			e.key === 'o' ? selectedSynth[12]?.triggerAttack('A#4') : '';
			keysDown = [...keysDown, e.key];
		}
	}

	function handleKeyUp(e: KeyboardEvent) {
		if (selectedSynth && keysDown.includes(e.key)) {
			e.key === 'a' ? selectedSynth[0]?.triggerRelease() : '';
			e.key === 's' ? selectedSynth[1]?.triggerRelease() : '';
			e.key === 'd' ? selectedSynth[2]?.triggerRelease() : '';
			e.key === 'f' ? selectedSynth[3]?.triggerRelease() : '';
			e.key === 'j' ? selectedSynth[4]?.triggerRelease() : '';
			e.key === 'k' ? selectedSynth[5]?.triggerRelease() : '';
			e.key === 'l' ? selectedSynth[6]?.triggerRelease() : '';
			e.key === ';' ? selectedSynth[7]?.triggerRelease() : '';
			e.key === 'w' ? selectedSynth[8]?.triggerRelease() : '';
			e.key === 'e' ? selectedSynth[9]?.triggerRelease() : '';
			e.key === 'u' ? selectedSynth[10]?.triggerRelease() : '';
			e.key === 'i' ? selectedSynth[11]?.triggerRelease() : '';
			e.key === 'o' ? selectedSynth[12]?.triggerRelease() : '';
			keysDown = keysDown.filter((keys) => keys !== e.key);
		}
	}
</script>

<div id="keyboard" tabindex="-1" on:keydown={handleKeyDown} on:keyup={handleKeyUp}>
	<div class="whiteKeys">
		<Key
			pitch={'C4'}
			text={'C'}
			synth={selectedSynth ? selectedSynth[0] : undefined}
			keydown={keysDown.includes('a') ? true : false}
		/>
		<Key
			pitch={'D4'}
			text={'D'}
			synth={selectedSynth ? selectedSynth[1] : undefined}
			keydown={keysDown.includes('s') ? true : false}
		/>
		<Key
			pitch={'E4'}
			text={'E'}
			synth={selectedSynth ? selectedSynth[2] : undefined}
			keydown={keysDown.includes('d') ? true : false}
		/>
		<Key
			pitch={'F4'}
			text={'F'}
			synth={selectedSynth ? selectedSynth[3] : undefined}
			keydown={keysDown.includes('f') ? true : false}
		/>
		<Key
			pitch={'G4'}
			text={'G'}
			synth={selectedSynth ? selectedSynth[4] : undefined}
			keydown={keysDown.includes('j') ? true : false}
		/>
		<Key
			pitch={'A4'}
			text={'A'}
			synth={selectedSynth ? selectedSynth[5] : undefined}
			keydown={keysDown.includes('k') ? true : false}
		/>
		<Key
			pitch={'B4'}
			text={'B'}
			synth={selectedSynth ? selectedSynth[6] : undefined}
			keydown={keysDown.includes('l') ? true : false}
		/>
		<Key
			pitch={'C5'}
			text={'C'}
			synth={selectedSynth ? selectedSynth[7] : undefined}
			keydown={keysDown.includes(';') ? true : false}
		/>
	</div>

	<div class="blackKeys">
		<div class="group2">
			<Key
				pitch={'C#4'}
				text={'C#/Db'}
				synth={selectedSynth ? selectedSynth[8] : undefined}
				keydown={keysDown.includes('w') ? true : false}
			/>
			<Key
				pitch={'D#4'}
				text={'D#/Eb'}
				synth={selectedSynth ? selectedSynth[9] : undefined}
				keydown={keysDown.includes('e') ? true : false}
			/>
		</div>
		<div class="group3">
			<Key
				pitch={'F#4'}
				text={'F#/Gb'}
				synth={selectedSynth ? selectedSynth[10] : undefined}
				keydown={keysDown.includes('u') ? true : false}
			/>
			<Key
				pitch={'G#4'}
				text={'G#/Ab'}
				synth={selectedSynth ? selectedSynth[11] : undefined}
				keydown={keysDown.includes('i') ? true : false}
			/>
			<Key
				pitch={'A#4'}
				text={'A#/Bb'}
				synth={selectedSynth ? selectedSynth[12] : undefined}
				keydown={keysDown.includes('o') ? true : false}
			/>
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

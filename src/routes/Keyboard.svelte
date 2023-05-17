<script lang="ts">
	import type * as Tone from 'tone';
	import Key from './Key.svelte';

	export let loadedSynth: (
		| Tone.Synth
		| Tone.AMSynth
		| Tone.DuoSynth
		| Tone.MembraneSynth
		| Tone.MetalSynth
		| Tone.MonoSynth
		| Tone.NoiseSynth
		| Tone.PluckSynth
	)[];

	let keysDown: string[] = [];

	function handleKeyDown(e: KeyboardEvent) {
		if (loadedSynth && !keysDown.includes(e.key)) {
			e.key === 'a' ? loadedSynth[0]?.triggerAttack('C4') : '';
			e.key === 's' ? loadedSynth[1]?.triggerAttack('D4') : '';
			e.key === 'd' ? loadedSynth[2]?.triggerAttack('E4') : '';
			e.key === 'f' ? loadedSynth[3]?.triggerAttack('F4') : '';
			e.key === 'j' ? loadedSynth[4]?.triggerAttack('G4') : '';
			e.key === 'k' ? loadedSynth[5]?.triggerAttack('A4') : '';
			e.key === 'l' ? loadedSynth[6]?.triggerAttack('B4') : '';
			e.key === ';' ? loadedSynth[7]?.triggerAttack('C5') : '';
			e.key === 'w' ? loadedSynth[8]?.triggerAttack('C#4') : '';
			e.key === 'e' ? loadedSynth[9]?.triggerAttack('D#4') : '';
			e.key === 'u' ? loadedSynth[10]?.triggerAttack('F#4') : '';
			e.key === 'i' ? loadedSynth[11]?.triggerAttack('G#4') : '';
			e.key === 'o' ? loadedSynth[12]?.triggerAttack('A#4') : '';
			keysDown = [...keysDown, e.key];
		}
	}

	function handleKeyUp(e: KeyboardEvent) {
		if (loadedSynth && keysDown.includes(e.key)) {
			e.key === 'a' ? loadedSynth[0]?.triggerRelease() : '';
			e.key === 's' ? loadedSynth[1]?.triggerRelease() : '';
			e.key === 'd' ? loadedSynth[2]?.triggerRelease() : '';
			e.key === 'f' ? loadedSynth[3]?.triggerRelease() : '';
			e.key === 'j' ? loadedSynth[4]?.triggerRelease() : '';
			e.key === 'k' ? loadedSynth[5]?.triggerRelease() : '';
			e.key === 'l' ? loadedSynth[6]?.triggerRelease() : '';
			e.key === ';' ? loadedSynth[7]?.triggerRelease() : '';
			e.key === 'w' ? loadedSynth[8]?.triggerRelease() : '';
			e.key === 'e' ? loadedSynth[9]?.triggerRelease() : '';
			e.key === 'u' ? loadedSynth[10]?.triggerRelease() : '';
			e.key === 'i' ? loadedSynth[11]?.triggerRelease() : '';
			e.key === 'o' ? loadedSynth[12]?.triggerRelease() : '';
			keysDown = keysDown.filter((keys) => keys !== e.key);
		}
	}
</script>

<div id="keyboard" tabindex="-1" on:keydown={handleKeyDown} on:keyup={handleKeyUp}>
	<div class="whiteKeys">
		<Key
			pitch={'C4'}
			text={'C'}
			synth={loadedSynth ? loadedSynth[0] : undefined}
			keydown={keysDown.includes('a') ? true : false}
		/>
		<Key
			pitch={'D4'}
			text={'D'}
			synth={loadedSynth ? loadedSynth[1] : undefined}
			keydown={keysDown.includes('s') ? true : false}
		/>
		<Key
			pitch={'E4'}
			text={'E'}
			synth={loadedSynth ? loadedSynth[2] : undefined}
			keydown={keysDown.includes('d') ? true : false}
		/>
		<Key
			pitch={'F4'}
			text={'F'}
			synth={loadedSynth ? loadedSynth[3] : undefined}
			keydown={keysDown.includes('f') ? true : false}
		/>
		<Key
			pitch={'G4'}
			text={'G'}
			synth={loadedSynth ? loadedSynth[4] : undefined}
			keydown={keysDown.includes('j') ? true : false}
		/>
		<Key
			pitch={'A4'}
			text={'A'}
			synth={loadedSynth ? loadedSynth[5] : undefined}
			keydown={keysDown.includes('k') ? true : false}
		/>
		<Key
			pitch={'B4'}
			text={'B'}
			synth={loadedSynth ? loadedSynth[6] : undefined}
			keydown={keysDown.includes('l') ? true : false}
		/>
		<Key
			pitch={'C5'}
			text={'C'}
			synth={loadedSynth ? loadedSynth[7] : undefined}
			keydown={keysDown.includes(';') ? true : false}
		/>
	</div>

	<div class="blackKeys">
		<div class="group2">
			<Key
				pitch={'C#4'}
				text={'C#/Db'}
				synth={loadedSynth ? loadedSynth[8] : undefined}
				keydown={keysDown.includes('w') ? true : false}
			/>
			<Key
				pitch={'D#4'}
				text={'D#/Eb'}
				synth={loadedSynth ? loadedSynth[9] : undefined}
				keydown={keysDown.includes('e') ? true : false}
			/>
		</div>
		<div class="group3">
			<Key
				pitch={'F#4'}
				text={'F#/Gb'}
				synth={loadedSynth ? loadedSynth[10] : undefined}
				keydown={keysDown.includes('u') ? true : false}
			/>
			<Key
				pitch={'G#4'}
				text={'G#/Ab'}
				synth={loadedSynth ? loadedSynth[11] : undefined}
				keydown={keysDown.includes('i') ? true : false}
			/>
			<Key
				pitch={'A#4'}
				text={'A#/Bb'}
				synth={loadedSynth ? loadedSynth[12] : undefined}
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

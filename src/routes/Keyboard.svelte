<script lang="ts">
	import type * as Tone from 'tone';
	import PowerButton from './PowerButton.svelte';
	import Key from './Key.svelte';

	let synthList: Tone.Synth[] | undefined = undefined;
	let keysDown: string[] = [];

	function handleSaveSynth(e: { detail: { synthList: Tone.Synth<Tone.SynthOptions>[] } }) {
		synthList = e.detail.synthList;
	}

	function handleKeyDown(e: KeyboardEvent) {
		if (synthList && !keysDown.includes(e.key)) {
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
			keysDown = [...keysDown, e.key];
		}
	}

	function handleKeyUp(e: KeyboardEvent) {
		if (synthList && keysDown.includes(e.key)) {
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
			keysDown = keysDown.filter((keys) => keys !== e.key);
		}
	}
</script>

<div id="keyboard" on:keydown={handleKeyDown} on:keyup={handleKeyUp}>
	<div class="whiteKeys">
		<Key
			pitch={'C4'}
			text={'C'}
			synth={synthList ? synthList[0] : undefined}
			keydown={keysDown.includes('a') ? true : false}
		/>
		<Key
			pitch={'D4'}
			text={'D'}
			synth={synthList ? synthList[1] : undefined}
			keydown={keysDown.includes('s') ? true : false}
		/>
		<Key
			pitch={'E4'}
			text={'E'}
			synth={synthList ? synthList[2] : undefined}
			keydown={keysDown.includes('d') ? true : false}
		/>
		<Key
			pitch={'F4'}
			text={'F'}
			synth={synthList ? synthList[3] : undefined}
			keydown={keysDown.includes('f') ? true : false}
		/>
		<Key
			pitch={'G4'}
			text={'G'}
			synth={synthList ? synthList[4] : undefined}
			keydown={keysDown.includes('j') ? true : false}
		/>
		<Key
			pitch={'A4'}
			text={'A'}
			synth={synthList ? synthList[5] : undefined}
			keydown={keysDown.includes('k') ? true : false}
		/>
		<Key
			pitch={'B4'}
			text={'B'}
			synth={synthList ? synthList[6] : undefined}
			keydown={keysDown.includes('l') ? true : false}
		/>
		<Key
			pitch={'C5'}
			text={'C'}
			synth={synthList ? synthList[7] : undefined}
			keydown={keysDown.includes(';') ? true : false}
		/>
	</div>

	<div class="blackKeys">
		<div class="group2">
			<Key
				pitch={'C#4'}
				text={'C#/Db'}
				synth={synthList ? synthList[8] : undefined}
				keydown={keysDown.includes('w') ? true : false}
			/>
			<Key
				pitch={'D#4'}
				text={'D#/Eb'}
				synth={synthList ? synthList[9] : undefined}
				keydown={keysDown.includes('e') ? true : false}
			/>
		</div>
		<div class="group3">
			<Key
				pitch={'F#4'}
				text={'F#/Gb'}
				synth={synthList ? synthList[10] : undefined}
				keydown={keysDown.includes('u') ? true : false}
			/>
			<Key
				pitch={'G#4'}
				text={'G#/Ab'}
				synth={synthList ? synthList[11] : undefined}
				keydown={keysDown.includes('i') ? true : false}
			/>
			<Key
				pitch={'A#4'}
				text={'A#/Bb'}
				synth={synthList ? synthList[12] : undefined}
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

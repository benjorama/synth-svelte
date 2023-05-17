<script lang="ts">
	import type * as Tone from 'tone';

	export let pitch: string;
	export let text: string;
	export let synth: Tone.Synth | Tone.AMSynth | undefined = undefined;
	export let keydown: boolean;

	let mousedown = false;

	function handleMouseDown() {
		synth ? synth.triggerAttack(pitch) : '';
		mousedown = true;
	}

	function handleMouseUp() {
		synth ? synth.triggerRelease() : '';
		let powerButton = document.getElementById('powerButton');
		powerButton ? powerButton.focus() : '';
		mousedown = false;
	}

	function handleOnKeyUp() {
		console.log('key up');
	}
	function handleOnKeyDown() {
		console.log('key down');
	}
	function handleOnKeyPress() {
		console.log('key press');
	}
</script>

{#if pitch.includes('#')}
	<div
		class={keydown || mousedown ? 'blackKey keyDown' : 'blackKey'}
		on:mousedown={handleMouseDown}
		on:mouseup={handleMouseUp}
		on:keyup={handleOnKeyUp}
		on:keydown={handleOnKeyDown}
		on:keypress={handleOnKeyPress}
	>
		<div class="keyContent">{text}</div>
	</div>
{:else}
	<div
		class={keydown || mousedown ? 'whiteKey keyDown' : 'whiteKey'}
		on:mousedown={handleMouseDown}
		on:mouseup={handleMouseUp}
		on:keyup={handleOnKeyUp}
		on:keydown={handleOnKeyDown}
		on:keypress={handleOnKeyPress}
	>
		<div class="keyContent">{text}</div>
	</div>
{/if}

<style>
	.blackKey {
		position: relative;
		box-sizing: border-box;
		width: 2em;
		height: 9em;
		margin-left: 1em;
		background-color: black;
		color: white;
		text-align: center;
		overflow-wrap: break-word;
		border: 1px solid #bbb;
	}

	.whiteKey {
		position: relative;
		box-sizing: border-box;
		width: 3em;
		height: 14em;
		background-color: white;
		border: 1px solid #bbb;
	}

	.keyDown {
		background-color: lime;
	}

	.keyContent {
		position: absolute;
		bottom: 0;
		width: inherit;
		text-align: center;
		user-select: none;
	}
</style>

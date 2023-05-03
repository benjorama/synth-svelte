<script lang="ts">
	import type * as Tone from 'tone';

	export let pitch: string;
	export let text: string;
	export let synth: Tone.Synth | undefined = undefined;

	function handleClick() {
		synth ? synth.triggerAttackRelease(pitch, '8n') : '';
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
		class="blackKey"
		on:click={handleClick}
		on:keyup={handleOnKeyUp}
		on:keydown={handleOnKeyDown}
		on:keypress={handleOnKeyPress}
	>
		<div class="keyContent">{text}</div>
	</div>
{:else}
	<div
		class="whiteKey"
		on:click={handleClick}
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

	.keyContent {
		position: absolute;
		bottom: 0;
		width: inherit;
		text-align: center;
	}
</style>

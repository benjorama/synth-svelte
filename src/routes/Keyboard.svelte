<script lang="ts">
	import BlackKey from './BlackKey.svelte';
	import PowerButton from './PowerButton.svelte';
	import WhiteKey from './WhiteKey.svelte';
</script>

<div>
	<PowerButton />
	<div class="whiteKeys">
		<WhiteKey pitch={'C4'} />
		<WhiteKey pitch={'D4'} />
		<WhiteKey pitch={'E4'} />
		<WhiteKey pitch={'F4'} />
		<WhiteKey pitch={'G4'} />
		<WhiteKey pitch={'A4'} />
		<WhiteKey pitch={'B4'} />
	</div>

	<div class="blackKeys">
		<div class="group2">
			<BlackKey pitch={'C#/Db4'} />
			<BlackKey pitch={'D#/Eb4'} />
		</div>
		<div class="group3">
			<BlackKey pitch={'F#/Gb4'} />
			<BlackKey pitch={'G#/Ab4'} />
			<BlackKey pitch={'A#/Bb4'} />
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
		left: 1em;
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

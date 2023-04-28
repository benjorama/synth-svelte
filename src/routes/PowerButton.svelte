<script>
	import * as Tone from 'tone';

	function handleClick() {
		//create a synth and connect it to the main output (your speakers)
		const synth = new Tone.Synth().toDestination();

		//play a middle 'C' for the duration of an 8th note
		synth.triggerAttackRelease('C4', '8n');
	}
</script>

<button on:click={handleClick}> click me! </button>

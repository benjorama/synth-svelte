<script lang="ts">
	export let pitch: string;
</script>

<div class="blackKey">{pitch}</div>

<style>
	.blackKey {
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
</style>

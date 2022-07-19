<script>
	import { getContext } from "svelte";
	let teams = getContext('teams');
	export let name;
</script>

<select class="team-selector" name={name}>
	<option disabled selected>Choose a team</option>

		{#each $teams as team}
		<option value="{team.name}">{team.location} {team.name}</option>
		{/each}
</select> 

<style>

	select {
		width: calc(100% - 1rem);
		font-size: 1.0rem;
		padding: 0.5rem;
		margin: 0.5rem;
		border-radius: 0.5rem;
	}

</style>
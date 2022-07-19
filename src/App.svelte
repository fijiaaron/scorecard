<script>
	import { onMount, setContext } from 'svelte'
	import { writable } from 'svelte/store'
	import Score from './lib/Score.svelte'
	import TeamSelector from './lib/TeamSelector.svelte'

	const teams = writable([]);
	setContext('teams', teams);

	onMount(fetchTeams);
	
	async function fetchTeams() {
		console.log("fetchTeams()...");
	
		try {
			const response = await fetch("/api/teams.json");
			console.log(response);
			const teams_json = await response.json();
			console.log("teams_json", teams_json);
			teams.set(teams_json);	
		}
		catch (e) {
			console.log("error", e);
		}
	}
  </script>

<div id="app">

	<header>
		<a href="/">
			<img src="/scorecard.svg" class="logo" alt="Scorecard Logo" />
			<h1 class="title">Scorecard</h1>
		</a>
	</header>


	<main>
		<div class="card" id="team1">
			<h2>Team 1</h2>
			<TeamSelector name="team1"/>

			<div class="justified">
				<Score forTeam="team1"/>
				<button>Reset</button>
			</div>
		</div>


		<div class="card" id="team2">
			<h2>Team 2</h2>
			<TeamSelector name="team2"/>

			<div class="justified">
				<Score forTeam="team2"/>
				<button>Reset</button>
			</div>
		</div>	
	</main>
</div>

<style>
	
	
	header {
		display: flex;
		flex-direction: row;
		justify-content: space-around;
		word-wrap: nowrap;
	}

	.logo {
		padding-right: 0.5ch;
	}

	.title {
		color: rgb(250, 75 , 25)
	}
	
	header .logo, header .title {
		display: inline-block;
		vertical-align: middle;
		height: 2rem;
		font-size: 2rem;
	}

	input, select, button {
		font-size: 1rem;
		padding: 0.5ch 1ch;
		margin: 0.5ch;
		border-radius: 0.5rem;
		width: 100%;
	}
	
	.justified {
		display: flex;
		flex-direction: row;
		justify-content: space-between;
	}

	.justified > * {
		display: inline;
		width: 50%;
	}

	.card {
		width: 100%;
	}
</style>

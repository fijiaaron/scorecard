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

		<footer>
			<div>&copy; 2022</div>
			<div>Privacy</div>
		</footer>

</div>

<style>
	
	#app {
		display: flex;
		flex-direction: column;
		min-height: 100vh;
		margin: 0;
	}

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
		font-size: 2rem;
		vertical-align: middle;

		border: 1px dotted gray;

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
		margin: 1em auto;
		padding: 1em;
		width: 50%;
		border: 1px dotted gray;
	}

	main {
		flex: 1;
		border: 1px dotted gray;
	}

	footer {
		display: flex;
		flex-direction: row;
		align-items: center;
		justify-content: space-between;
		padding: 1em;
		border: 1px solid black;
		min-width: 320px;
	}

	footer div {
		display: inline-block;
	}

	
</style>

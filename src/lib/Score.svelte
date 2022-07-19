<script>
  import { getContext } from "svelte";
	let teams = getContext('teams');
	
  export let forTeam;
	
  let score = 0
  const increment = () => {
    score += 1
  }
</script>

<button on:click={increment}>
  {forTeam} : {score}
</button>

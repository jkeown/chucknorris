<script>
import {createEventDispatcher} from 'svelte';

const dispatch = createEventDispatcher();

let numJokes = 1;

function sendJokeCount(){
    dispatch('jokes',{
        count: numJokes
    });
}
</script>

<form on:submit|preventDefault class="bg-orange-100 p-5 my-5 shadow-xs  w-4/5 md:w-1/2 text-center">
  <label for="numJokes">I would like 
	<input class="pl-2 w-10 border-b border-orange-500" id="numJokes" type="number" min="1" max="5" bind:value={numJokes}>
	kick butt {numJokes === 1 ? 'joke' : 'jokes'}!</label>
	<button class="font-bold border-2 border-orange-500 rounded p-2 m-2 hover:bg-orange-500 hover:text-white" 
	on:click={sendJokeCount}>Get {numJokes} {numJokes === 1 ? 'Joke' : 'Jokes'}
	</button>
  </form>
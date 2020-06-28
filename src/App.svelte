<script>
import { fade, fly } from 'svelte/transition';
import Header from './Header.svelte';
import Form from './Form.svelte';
import Footer from './Footer.svelte';
 
  const getRandomJoke = "https://api.icndb.com/jokes/random";
  let jokes = [];
  let isLoading = false;

  function getLaughs(event) {
    let numJokes = event.detail.count;
	  jokes = [];
	  isLoading = true;
    fetch(`${getRandomJoke}/${numJokes > 5 ? 5: numJokes}?limitTo=[nerdy]`)
	  .then(res => 
	  res.json())
      .then(data => {
		  console.log(data);
		  isLoading = false;
        data.value.forEach(joke => jokes.push(joke.joke));
	  })
	  .catch(err => console.log(err));
  }
</script>


<Header />
<main class="flex flex-col items-center flex-grow">

<Form on:jokes={getLaughs}/>

<div class="h-8">
  {#if isLoading}
  <div in:fly={ {x: -300} } out:fade class="flex items-baseline">
  <p class="font-bold">Jokes are on the way ...</p>
  <img src="img/karate.svg" alt="karate kick" width="50">
  </div>
  {/if}
</div>
  {#if !isLoading}
	  <ul class="w-4/5 md:w-1/2">
	  {#each jokes as joke}
	  <li class="py-6 px-12">{@html joke}</li>
	  {/each}
	  </ul>
  {/if}
  
</main>

<Footer />



<style>
  li{
	  background: url('../img/icons8-color-hand-drawn-50.png') left center no-repeat;
  }
</style>
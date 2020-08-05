<script>
  import { onMount } from 'svelte';
  import { fade } from 'svelte/transition/';
  import { fetchActor } from '../api';

  // Component
  import NavigationPerson from '../components/NavigationPerson.svelte';
  import Spinner from '../components/Spinner.svelte';
  import PersonInfo from '../components/PersonInfo.svelte';
  import Grid from '../components/Grid.svelte';
  import ThumbMovie from '../components/ThumbMovie.svelte';

  export let params;

  let isLoading;
  let error;
  let actor;

  const handleFetchActor = async () => {
    try {
        isLoading = true;
        error = false;
        actor = await fetchActor(params.id);
    } catch (err) {
        error = true;
    }
    isLoading= false;
};

onMount(async () => {
  const localActor = window.localStorage.getItem(params.id);
    if (localActor) {
      console.log('Grabbing from localStorage');
      actor = JSON.parse(localActor);
    } else {
      console.log('Grabbing from API.');
    handleFetchActor();
    }
});

$: {
    if (actor) {
      window.localStorage.setItem(params.id, JSON.stringify(actor));
    }
  }

</script>

{#if error}
  <p>Something went wrong ...</p>
{:else if actor}
  <div transition:fade={{ duration: 300 }}>
    <NavigationPerson actor={actor.name} />
    <PersonInfo {actor}  />
    <Grid header="Film" >
      {#each actor.movie_credits as movie }
          <ThumbMovie {movie} movieId={movie.id}/>
      {/each}
  </Grid>
  </div>
{/if}

{#if isLoading}
  <Spinner />
{/if}

<style>

</style>
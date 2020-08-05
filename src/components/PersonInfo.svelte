<script>
  // com
  import ThumbPerson from '../components/Thumb.svelte';
  // config
  import { POSTER_SIZE, IMAGE_BASE_URL, BACKDROP_SIZE } from '../config';

  const noImage = '/images/no_image.jpg';
  export let actor;
</script>

<div class="wrapper">
<div class="content">
    <div class="thumb">
      <ThumbPerson
        image={actor.profile_path ? `${IMAGE_BASE_URL}${POSTER_SIZE}${actor.profile_path}` : noImage} alt="actorthumb"} />
    </div>
    <div class="text">
      <h1>{actor.name}</h1>
      <h3>Biography</h3>
      <p>{actor.biography}</p>
      <h3>Birthday : {actor.birthday}</h3>
      <h3>Place of Birth : {actor.place_of_birth}</h3>
      <h3>Popularity : {actor.popularity}</h3>

    </div>
  </div>
</div>

<style>
  .wrapper {
    background: silver;
    background-size: cover;
    background-position: center;
    padding: 40px 20px;
  }

  .content {
    display: flex;
    max-width: 1280px;
    max-height: 850px;
    margin: 0 auto;
    background: rgb(0, 0, 0, 0.7);
    border-radius: 20px;
  }

  .text {
    width: 70%;
    padding: 40px;
    color: #fff;
    overflow: hidden;
  }

  h1 {
    font-family: 'Abel', sans-serif;
    font-size: 48px;
    margin: 0;
  }

  h3 {
    font-size: 16px;
    line-height: 0;
    margin-top: 30px;
  }

  p {
    font-family: 'Abel', sans-serif;
    font-size: 18px;
    line-height: 26px;
  }

  
  @media screen and (max-width: 768px) {
    .content {
      display: block;
      max-height: none;
    }
  }

  @media screen and (max-width: 1000px) {
    h1 {
      font-size: 32px !important;
    }
  }
</style>
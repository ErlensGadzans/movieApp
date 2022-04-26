<template>
  <div class="container single-movie">
    <NuxtLink class="button" :to="{ name: 'index' }">Back</NuxtLink>
    <div class="movie-info">
      <div class="movie-img">
        <img
          :src="`https://image.tmdb.org/t/p/w500/${this.movie.poster_path}`"
          alt=""
        />
      </div>
      <div class="movie-content">
        <h1>Title: {{ this.movie.title }}</h1>
        <p class="movie-fact tagline">
          <span>Tagline:</span> "{{ this.movie.tagline }}"
        </p>
        <p class="movie-fact">
          <span>Released:</span>
          {{ this.movie.release_date }}
        </p>
        <p class="movie-fact">
          <span>Duration:</span> {{ this.movie.runtime }} minutes
        </p>
        <p class="movie-fact">
          <span>Overview:</span> {{ this.movie.overview }}
        </p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'single-movie',
  data() {
    return {
      movie: '',
    }
  },

  async fetch() {
    const data = await fetch(
      `https://api.themoviedb.org/3/movie/${this.$route.params.movieid}?api_key=&language=en-US`
    )
    const response = await data.json()
    // console.log(response, 'response single movie')

    this.movie = response
    // console.log(this.movie, 'MOVIE')
  },
}
</script>

<style lang="scss" scoped>
.single-movie {
  color: #fff;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding: 32px 16px;
  .button {
    align-self: flex-start;
    margin-bottom: 32px;
  }
  .movie-info {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 32px;
    color: #fff;
    @media (min-width: 800px) {
      flex-direction: row;
      align-items: flex-start;
    }
    .movie-img {
      img {
        max-height: 500px;
        width: 100%;
        @media (min-width: 800px) {
          max-height: 700px;
          width: initial;
        }
      }
    }
    .movie-content {
      h1 {
        font-size: 56px;
        font-weight: 400;
      }
      .movie-fact {
        margin-top: 12px;
        font-size: 20px;
        line-height: 1.5;
        span {
          font-weight: 600;
          text-decoration: underline;
        }
      }
      .tagline {
        font-style: italic;
        span {
          font-style: normal;
        }
      }
    }
  }
}
</style>
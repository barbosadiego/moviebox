<template>
  <section class="hero">
    <div class="hero__slider">
      <div class="item" v-for="film in top_rated" :key="film.id">
        <img
          :src="`https://image.tmdb.org/t/p/w1280/${film.backdrop_path}`"
          :alt="film.title"
        />
        <div class="info">
          <h2>{{ film.title }}</h2>
          <p>{{ film.overview }}</p>
          <button>
            <svg
              width="20"
              height="20"
              viewBox="0 0 20 20"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                fill-rule="evenodd"
                clip-rule="evenodd"
                d="M10 18C14.4183 18 18 14.4183 18 10C18 5.58172 14.4183 2 10 2C5.58172 2 2 5.58172 2 10C2 14.4183 5.58172 18 10 18ZM9.5547 7.16795C9.24784 6.96338 8.8533 6.94431 8.52814 7.11833C8.20298 7.29235 8 7.63121 8 8V12C8 12.3688 8.20298 12.7077 8.52814 12.8817C8.8533 13.0557 9.24784 13.0366 9.5547 12.8321L12.5547 10.8321C12.8329 10.6466 13 10.3344 13 10C13 9.66565 12.8329 9.35342 12.5547 9.16795L9.5547 7.16795Z"
                fill="white"
              />
            </svg>
            watch trailer
          </button>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'HeroComponent',
  data() {
    return {
      top_rated: [],
    };
  },
  methods: {
    async getPopularFilms() {
      try {
        const data = await fetch(
          'https://api.themoviedb.org/3/movie/popular?api_key=9c9812be1a1ba5a02119cd027ce578f2',
        );
        const response = await data.json();
        if (data.ok) {
          this.top_rated = response.results.slice(0, 5);
          console.log(this.top_rated);
        }
      } catch (error) {
        console.log(error);
      }
    },
  },
  created() {
    this.getPopularFilms();
  },
};
</script>

<style lang="scss" scoped>
@import '@/Functions';

.hero {
  button {
    display: flex;
    align-items: center;
    gap: 8px;
    background-color: var(--rose);
    border: none;
    height: 36px;
    cursor: pointer;
    padding: 6px 16px;
    border-radius: 6px;
    color: var(--text-color);
    font-size: rem(14px);
    font-weight: 700;
    text-transform: uppercase;
  }

  &__slider {
    position: relative;
    top: -80px;

    .item {
      position: relative;
      display: grid;
      grid-template-columns: 1fr minmax(400px, 1240px) 1fr;
      height: 600px;

      &::before {
        grid-column: 1/-1;
        content: '';
        display: block;
        width: 100%;
        height: 100%;
        background-image: linear-gradient(
            180deg,
            rgba(0, 0, 0, 0.7) 10%,
            transparent 95%
          ),
          linear-gradient(90deg, rgba(0, 0, 0, 0.7), transparent);
        position: absolute;
        top: 0px;
        left: 0px;
      }

      img {
        width: 100%;
        height: 600px;
        object-fit: cover;
        grid-column: 1/-1;
      }

      .info {
        grid-column: 2/3;
        position: absolute;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: flex-start;
        gap: 1rem;
        width: 100%;
        height: 100%;
        color: var(--text-color);
        padding: 0px 95px;
        max-width: 600px;

        h2 {
          font-size: rem(48);
          line-height: rem(56);
          font-weight: 700;
          margin-bottom: 1rem;
        }

        p {
          font-size: rem(14);
          line-height: rem(18);
          font-weight: 500;
        }
      }
    }
  }
}
</style>
<template>
  <section class="hero">
    <div class="hero__slider">
      <div class="item" data-slide v-for="film in top_rated" :key="film.id">
        <img
          :src="`https://image.tmdb.org/t/p/w1280/${film.backdrop_path}`"
          :alt="film.title"
        />
        <div class="info">
          <h2>{{ film.title }}</h2>
          <div class="popularity">
            <span class="imdb">
              <img src="@/assets/imdb.png" alt="" width="35" height="17" />
              <span>{{ Math.round(film.popularity) }}</span>
            </span>
            <span class="vote">
              <img
                src="@/assets/tomato-icon.png"
                alt=""
                width="16"
                height="17"
              />
              <span>{{ film.vote_average }}</span>
            </span>
          </div>
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
      <div class="index">
        <button data-index>1</button>
        <button data-index>2</button>
        <button data-index>3</button>
        <button data-index>4</button>
        <button data-index>5</button>
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
      index: 0,
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
        }
      } catch (error) {
        console.log(error);
      }
    },
    activeSlide() {
      const items = document.querySelectorAll('[data-slide]');
      const indexIndicators = document.querySelectorAll('[data-index]');
      items[0].classList.add('active');
      indexIndicators[0].classList.add('active');

      setInterval(() => {
        this.index === items.length - 1 ? (this.index = 0) : this.index++;
        items.forEach((slide) => slide.classList.remove('active'));
        indexIndicators.forEach((indicator) =>
          indicator.classList.remove('active'),
        );
        items[this.index].classList.add('active');
        indexIndicators[this.index].classList.add('active');
      }, 5000);
    },
  },
  created() {
    this.getPopularFilms();
  },
  updated() {
    this.activeSlide();
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
    display: grid;
    grid-template-columns: 1fr minmax(400px, 1240px) 1fr;
    align-items: center;
    justify-items: end;
    height: 600px;
    width: 100%;
    @media screen and (max-width: 500px) {
      grid-template-columns: 1fr;
      align-items: flex-end;
      justify-items: center;
      max-height: 100vh;
    }

    .item {
      position: absolute;
      height: 600px;
      width: 100%;
      opacity: 0;
      display: grid;
      grid-template-columns: 1fr minmax(400px, 1240px) 1fr;
      transition: opacity 0.5s;
      z-index: -1;
      &.active {
        opacity: 1;
        user-select: unset;
        z-index: 5;
      }

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
        object-position: center;
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
        @media screen and (max-width: 768px) {
          padding: 15px 30px;
          max-width: 400px;
        }
        @media screen and (max-width: 500px) {
          padding: 15px;
        }

        h2 {
          font-size: rem(48);
          line-height: rem(56);
          font-weight: 700;
          margin-bottom: 1rem;
        }

        .popularity {
          display: flex;
          align-items: center;
          gap: 35px;

          & > span {
            display: flex;
            align-items: center;
            gap: 10px;
          }

          img {
            max-width: 35px;
            height: 17px;
          }
        }

        p {
          font-size: rem(14);
          line-height: rem(18);
          font-weight: 500;
          @media screen and (max-width: 500px) {
            max-width: 30ch;
          }
        }
      }
    }

    .index {
      position: relative;
      grid-column: 2/3;
      padding: 0px 95px;
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 10px;
      z-index: 5;
      @media screen and (max-width: 768px) {
        padding: 15px 30px;
      }
      @media screen and (max-width: 500px) {
        grid-column: 1;
        flex-direction: row;
        align-items: flex-end;
      }

      button {
        color: var(--gray-400);
        font-size: rem(12);
        font-weight: 700;
        line-height: rem(14);
        position: relative;
        display: flex;
        align-items: center;
        background-color: transparent;
        padding: 0px 10px;

        &.active {
          color: var(--text-color);
          font-size: rem(14);
          &::before {
            position: absolute;
            left: -26px;
            content: '';
            display: inline-block;
            width: 20px;
            height: 3px;
            border-radius: 6px;
            background-color: var(--white);
            @media screen and (max-width: 500px) {
              left: 12px;
              top: -14px;
              width: 3px;
              height: 20px;
            }
          }
        }
      }
    }
  }
}
</style>

<template>
  <header class="header">
    <nav class="header__nav container">
      <div class="logo">
        <img src="@/assets/Logo.svg" alt="" />
      </div>
      <div :class="['search', { active: isMenuMobile }]">
        <input
          type="text"
          name="search"
          id="search"
          placeholder="What do you want do watch?"
        />
        <img src="@/assets/Search.svg" alt="" />
      </div>
      <div :class="['signin', { active: isMenuMobile }]">
        <span>sing in</span>
        <button class="menu-area" @click="handleActive">
          <div class="menu"></div>
        </button>
      </div>
    </nav>
  </header>
</template>

<script>
export default {
  name: 'HeaderComponent',
  data() {
    return {
      isMenuMobile: false,
    };
  },
  methods: {
    handleActive() {
      const mdQuerie = window.matchMedia('(max-width: 768px)');
      if (mdQuerie.matches) {
        this.isMenuMobile = !this.isMenuMobile;
      }
    },
  },
};
</script>

<style lang="scss" scoped>
@import '@/Functions';

.header {
  background-color: transparent;
  position: relative;
  z-index: 10;

  &__nav {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 50px;
    color: var(--text-color);
    padding: 15px 95px;
    @media screen and (max-width: 860px) {
      padding: 15px;
    }

    .logo {
      height: 50px;
    }

    .search {
      flex: 1 0 270px;
      max-width: 525px;
      position: relative;
      display: flex;
      justify-content: space-between;
      border: 2px solid var(--border-color);
      padding: 6px 10px;
      border-radius: 6px;
      @media screen and (max-width: 768px) {
        display: none;
      }

      input {
        width: 100%;
        background-color: transparent;
        border: none;
        padding: 6px 10px;
        outline: none;
        color: var(--text-color);

        &::placeholder {
          font-family: inherit;
          color: var(--text-color);
          font-size: rem(16);
          line-height: rem(24);
        }
      }

      //search
      &.active {
        display: flex;
        position: absolute;
        top: 100px;
        left: 50%;
        transform: translateX(-50%);
        background-color: rgba(0, 0, 0, 0.9);
        z-index: 10;
        width: 90%;
        &::before {
          content: '';
          position: absolute;
          width: 150vw;
          top: -102px;
          left: -50%;
          right: 0px;
          height: 600px;
          background-color: rgba(0, 0, 0, 0.9);
          z-index: -1;
        }
      }
    }

    .signin {
      display: flex;
      align-items: center;
      gap: 27px;

      span {
        display: inline-block;
        font-size: rem(16);
        font-weight: 700;
        line-height: rem(24);
        text-transform: capitalize;
        @media screen and (max-width: 768px) {
          display: none;
        }
      }

      .menu-area {
        width: 36px;
        height: 36px;
        background-color: var(--rose);
        display: flex;
        align-items: center;
        justify-content: center;
        border-radius: 50%;
        border: none;
        cursor: pointer;
        z-index: 10;

        .menu {
          display: inline-block;
          width: 20px;
          height: 3px;
          background-color: var(--white);
          border-radius: 2px;
          box-shadow: 0px 10px var(--white);
          transform: translateY(-5px);
          transition: 0.2s;
        }
      }

      &.active .menu-area .menu {
        transform: rotate(45deg);
        box-shadow: none;
        position: relative;
        &::before {
          content: '';
          width: 20px;
          height: 3px;
          background-color: var(--white);
          border-radius: 2px;
          position: absolute;
          top: 0px;
          left: 0px;
          transform: rotate(-90deg);
        }
      }
    }
  }
}
</style>

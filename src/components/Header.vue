<template>
  <header class="header">
    <nav class="header__nav container">
      <div class="logo">
        <img src="@/assets/Logo.svg" alt="" />
      </div>
      <div class="search">
        <input
          type="text"
          name="search"
          id="search"
          placeholder="What do you want do watch?"
        />
        <img src="@/assets/Search.svg" alt="" />
      </div>
      <div class="signin">
        <span>sing in</span>
        <div class="menu-area">
          <div class="menu"></div>
        </div>
      </div>
    </nav>
  </header>
</template>

<script>
export default {
  name: 'HeaderComponent',
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
      }

      .menu-area {
        width: 36px;
        height: 36px;
        background-color: var(--rose);
        display: flex;
        align-items: center;
        justify-content: center;
        border-radius: 50%;
        cursor: pointer;

        .menu {
          display: inline-block;
          width: 20px;
          height: 3px;
          background-color: var(--white);
          border-radius: 2px;
          box-shadow: 0px 10px;
          transform: translateY(-5px);
        }
      }
    }
  }
}
</style>

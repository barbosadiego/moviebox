<template>
  <div id="app">
    <Header />
    <Hero />
  </div>
</template>

<script>
import Header from '@/components/Header.vue';
import Hero from '@/components/Hero.vue';

export default {
  components: {
    Header,
    Hero,
  },
};
</script>

<style lang="scss">
:root {
  --text-color: #fff;
  --border-color: #d1d5db;
  --rose: #e11d48;
  --white: #fff;
  --gray: #374151;
  --gray-400: #9ca3af;
}

* {
  box-sizing: border-box;
}

img {
  max-width: 100%;
  display: block;
}

body,
h1,
h2,
h3,
p,
ul,
li {
  margin: 0px;
  padding: 0px;
  font-family: 'DM Sans';
}

.container {
  max-width: 1240px;
  margin: 0 auto;
}

body {
  &::-webkit-scrollbar {
    width: 8px;
    background: var(--gray);
  }

  &::-webkit-scrollbar-thumb {
    background: var(--rose);
    border-radius: 4px;

    &:hover {
      background: lighten(#e11d48, $amount: 10%);
    }
  }
}

#app {
  overflow: hidden;
}
</style>

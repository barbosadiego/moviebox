<template>
  <div id="app">
    <Header />
  </div>
</template>

<script>
import Header from '@/components/Header.vue';

export default {
  components:{
    Header,
  }
}
</script>

<style lang="scss">
:root{
  --text-color: #fff;
  --border-color: #D1D5DB;
  --rose: #E11D48;
  --white: #fff;
}

*{
  box-sizing: border-box;
}

img{
  max-width: 100%;
  display: block;
}

body, h1, h2, h3, p, ul, li {
  margin: 0px;
  padding: 0px;
  font-family: 'DM Sans';
}

.container{
  max-width: 1240px;
  margin: 0 auto;
}


</style>

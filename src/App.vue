<script>
import Header from './components/Header.vue'


  export default {
    components: {
      Header,
    },
  }
</script>

<template>
  <div class="container">
    <Header/>
    <router-view></router-view>
  </div>
</template>

<style lang="scss" scoped>
.container{
  width: 70%;
  margin: 0 auto;
}
</style>
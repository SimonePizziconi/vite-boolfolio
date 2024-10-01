<script>
import NavBar from './partials/NavBar.vue';
import router from '../router/index';
    export default{
        components: {
            NavBar
        }
    }
</script>

<template>
    <header>
        <NavBar/>
        <router-view></router-view>
    </header>
</template>

<style lang="scss" scoped>
    header{
        height: 500px;
        width: 100%;
    }
</style>
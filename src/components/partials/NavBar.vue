<script>
    export default {
        
    }
</script>

<template>
    <nav>
        <ul>
            <li>
                <router-link :to="{name:home}">Home</router-link>
            </li>
            <li>
                <router-link :to="{name:projects}">Progetti</router-link>
            </li>
        </ul>
    </nav>
</template>

<style lang="scss" scoped>
    nav{
        width: 100;
        height: 80px;
        border-bottom: 0.5px solid lightblue;

        ul{
            height: 100%;
            width: 70%;
            margin: 0 auto;
            display: flex;
            align-items: center;
            justify-content: space-between;
        }
    }
</style>
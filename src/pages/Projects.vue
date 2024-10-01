<script>
import axios from 'axios';
import { store } from '@/store/store';
import Loading from '@/components/partials/Loading.vue';


    export default {
        name: 'Projects',
        components: {
            Loading
        },
        data() {
            return {
                projects: [],
                isLoading: true
            }
        },
        methods: {
            getApi() {
                axios.get( store.apiUrl + 'progetti')
                    .then(result => {
                        this.isLoading = false;
                        this.projects = result.data.results;
                    })
                    .catch(error => {
                        console.error(error); 
                    });
            }
        },
        mounted(){
            this.getApi();
        }
    }
</script>

<template>
    <h1>Progetti</h1>
    <div v-if="isLoading" class="loading">
        <Loading/>
    </div>
    <div v-else class="container-flex">
        <div class="card" v-for="project in projects" :key="project.id">
            <h1>Titolo: {{ project.title }}</h1>
            <div class="img-container">
                <img :src="project.image" alt="">
            </div>
            <p>Descrizione: {{ project.description }}</p>
            <span>Tipo: <span class="label">{{ project.type.name }}</span></span>
            <br>
            <span>Technologie: <span v-for="technology in project.technologies" :key="technology.id" class="label">{{ technology.name }}</span></span>
        </div>
    </div>
</template>

<style lang="scss" scoped>
    .loading{
        position: fixed;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            background-color: #f0f0f0; /* Puoi scegliere il colore di sfondo */
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 9999; /* Fa sì che stia sopra tutto */
    }

    .container-flex{
        width: 100%;
        display: flex;       
        gap: 20px;
        flex-wrap: wrap;

        .card{
            width: calc(100% / 3 - 20px);
            border-radius: 20px;
            border: 1px solid lightcyan;
            padding: 10px;

            .img-container{
                width: 100%;

                img{
                    width: 100%;
                }
            }
            .label{
                background-color: blue;
                padding: 5px;
                border-radius: 5px;
            }
        }
    }
</style>
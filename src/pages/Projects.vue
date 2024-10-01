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
            isLoading: true,
            activeDotIndex: null,  
            paginatorData: {
                links: []
            }
        };
    },
    methods: {
        getApi(url = store.apiUrl + 'progetti') {  
            this.isLoading = true;  
            axios.get(url)
                .then(result => {
                    this.paginatorData.links = result.data.results.links;
                    this.projects = result.data.results.data;
                    this.isLoading = false; 
                })
                .catch(error => {
                    console.error(error); 
                    this.isLoading = false;  
                });
        },
        handleDotClick(index, url) {
            this.setActiveDot(index);  
            if (url) {
                this.getApi(url); 
            }
        },
        setActiveDot(index) {
            this.activeDotIndex = index;  
        },
    },
    mounted(){
        this.getApi();  
    }
};
</script>


<template>
    <h1>Progetti</h1>
    <div v-if="isLoading" class="loading">
        <Loading />
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
            <span>Technologie: 
                <span v-for="technology in project.technologies" :key="technology.id" class="label">{{ technology.name }}</span>
            </span>
        </div>
    </div>

    <div class="pagination">
          
        <div v-for="(link, index) in paginatorData.links" 
             :key="index"
             :data-tooltip="link.label"
             class="pagination dot"
             :class="{ active: activeDotIndex === index }"
             @click="handleDotClick(index, link.url)"
            >
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
            background-color: #f0f0f0; 
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 9999; 
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

    // SCSS DEL PAGINATORE
    .pagination {
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    height: 15px;
    margin: auto;
    text-align: center;
    
    .dot {
        position: relative;
        width: 15px;
        height: 15px;
        border: 2px solid lighten(#1BA39C, 25%);
        border-radius: 100px;
        display: inline-block;
        cursor: pointer;
        margin: 0 4px;
        transition: .3s;
        
            &:first-child {
                display: none; // Nascondi il primo elemento
            }

            &:last-child {
                display: none; // Nascondi l'ultimo elemento
            }

            &.active {
                background: lighten(#1BA39C, 25%);
            }
            
            &:hover {
                transition: .3s;
                border-color: lighten(#1BA39C, 70%);
                background: lighten(#1BA39C, 70%);
                
                &:before {
                    top: -48px;
                    opacity: 1;
                }
            
                &:after {
                    top: -18px; 
                    opacity: 1;
                }
            }
            
            &:before {
                position: absolute;
                top: -40px;
                left: -36px;
                background: lighten(#1BA39C, 80%);
                width: 80px;
                font-family: "Montserrat";
                font-size: 14px;
                padding: 8px 0;
                border-radius: 3px;
                content: attr(data-tooltip);
                opacity: 0;
                transition: .3s;
            }
            
            &:after {
                position: absolute;
                width: 0;
                height: 0;
                top: -10px;
                left: -2px;
                border-top: 6px solid lighten(#1BA39C, 80%);
                border-right: 6px solid transparent;
                border-bottom: 6px solid transparent;
                border-left: 6px solid transparent;      
                content: "";
                opacity: 0;
                transition: .3s;
            }
        }
    }
</style>
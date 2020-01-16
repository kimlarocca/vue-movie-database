<template>
    <div class="movie-card" @click="toggleDetails">
        <img :src="'https://image.tmdb.org/t/p/w500'+image" :alt="title">
        <h2>{{ title | uppercase }}</h2>
        <div class="details" v-if="visible">
            <a class="button">X</a>
            <p>{{ overview }}</p>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'MovieCard',
        props: {
            title: String,
            image: String,
            visible: {
                type: Boolean,
                default: false
            },
            overview: String
        },
        methods: {
            toggleDetails () {
                this.visible = !this.visible
            }
        },
        filters: {
            uppercase(str){
                return str.toUpperCase()
            }
        }
    }
</script>

<style scoped>
    img {
        max-width: 100%;
        height: auto;
    }

    .movie-card {
        position: relative;
        cursor: pointer;
        opacity: 1;
        transition: .2s all linear;
        max-height: 281px;
    }

    .movie-card:hover {
        opacity: .8;
    }

    h2 {
        position: absolute;
        bottom: 20px;
        left: 20px;
        color: white;
        text-shadow: 1px 1px 0 #000;
        margin: 0;
    }

    .details {
        position: absolute;
        width: calc(100% - 40px);
        top: 0;
        bottom: 0;
        right: 0;
        left: 0;
        background: rgba(0, 0, 0, .85);
        color: white;
        padding: 30px 20px 20px;
        z-index: 10;
        text-align: left;
        font-size: .875rem;
    }

    .button {
        position: absolute;
        top: 0;
        right: 0;
        color: white;
        font-weight: bold;
        border-radius: 0;
        padding: 10px;
    }
</style>

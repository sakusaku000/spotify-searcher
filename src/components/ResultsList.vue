<template>
    <div class="results">
        <div class="head">
             <h1>{{results.length}} {{(results.length === 1) ? "Result" : "Results"}} for "{{searchTerm}}"</h1>
            <a href="/">New search</a>
        </div>
        <Track v-for="track in results" v-bind:key="track.id" :track="track"/>
    </div>
</template>

<script>
import Track from './Track.vue';

export default {
    name:"ResultsList",
    props:{
        searchTerm:String,
        results:Array
    },
    components:{
        Track
    }
}
</script>

<style scoped>
    .head {
        display:flex;
        justify-content:space-between;
        align-items:center;
    }

    a {
        padding:10px 20px;
        background-color:var(--color-accent);
        color:var(--color-main);
        font-family:inherit;
        outline:none;
        border:none;
        border-radius:10px;
        transition-duration:0.1s;
        text-decoration:none;
    }
    a:hover {
        background-color:var(--color-accent-hover);
        cursor:pointer;
    }
</style>
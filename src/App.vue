<template>
    <div class="container" v-if="authed">

        <Header/>

        <Search v-if="!searching" @search="search($event)"/>
        <h3 v-if="searchError">{{searchError}}</h3>

        <ResultsList v-if="results" :searchTerm="searchTerm" :results="results"/>
    </div>
</template>

<script>
// components
import Header from './components/Header.vue';
import Search from './components/Search.vue';
import ResultsList from './components/ResultsList.vue';

// modules
import axios from 'axios';
import qs from 'qs';

export default {
    name:"App",
    components:{
        Header,
        Search,
        ResultsList
    },
    data() {
        return {
            authed:false,
            searching:false,
            searchError:null,
            searchTerm:"",
            results:null
        }
    },
    created() {
        const vm = this;

        if (!localStorage.getItem("spotify_token")) {
            axios.post(`https://accounts.spotify.com/api/token`, qs.stringify({
                "grant_type":"client_credentials"
            }),
            {
                headers:{
                    "Content-Type":"application/x-www-form-urlencoded",
                    "Authorization":`Basic ${btoa(`${process.env.VUE_APP_SPOTIFY_CLIENT_ID}:${process.env.VUE_APP_SPOTIFY_CLIENT_SECRET}`)}`
                }
            }).then(res => {
                localStorage.setItem("spotify_token", res.data.access_token);
                vm.authed = true;
            }).catch(err => {
                console.error(err);
            });
        } else {
            this.authed = true;
        }
    },
    methods:{
        search(track) {
            const vm = this;
            this.searching = true;

            axios.get(`https://api.spotify.com/v1/search?q=${track}&type=track`, {
                headers:{
                    "Authorization":`Bearer ${localStorage.getItem("spotify_token")}`
                }
            }).then(res => {
                vm.searchTerm = track;
                vm.results = res.data.tracks.items;
                console.log(res.data.tracks.items);
            }).catch(err => {
                console.error(err);
                vm.searchError = err.message;
            });
        }
    }
}
</script>
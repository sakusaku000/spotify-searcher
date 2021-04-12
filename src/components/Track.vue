<template>
    <div class="track">
        <img :src="track.album.images[0].url">
        <div>
            <a :href="track.external_urls.spotify" target="_blank">
                <h1>{{track.name}}</h1>
                <h3>{{track.artists.map(a => `${a.name}`).join(", ")}}</h3>
            </a>
            <audio :id="track.id" :src="track.preview_url" controls/>
        </div>
    </div>
</template>

<script>
export default {
    name:"Track",
    props:{
        track:Object
    }
}
</script>

<style scoped>
    .track {
        display:flex;
        align-items:center;

        padding:30px 40px;
        margin-bottom:20px;
        border-radius:10px;

        background-color:var(--color-bg-secondary);
    }
    img {
        height:180px;
        margin-right:30px;
        border-radius:10px;
    }
    h1 {
        margin-bottom:0px;
    }
    h3 {
        margin-top:0px;
    }
    a {
        color:inherit;
        text-decoration:none;
    }
</style>
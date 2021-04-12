<template>
    <div class="search">
        <h3>Search for a track</h3>
        <form @submit.prevent="submitSearch">
            <input type="text" v-model="trackInput"/>
            <button type="submit">Search</button>
        </form>
    </div>
</template>

<script>
export default {
    name:"Search",
    data() {
        return {
            trackInput:""
        }
    },
    methods:{
        submitSearch() {            
            if (this.trackInput.length > 1) {
                this.$emit("search", this.trackInput);
                this.trackInput = "";
            };
        }
    }
}
</script>

<style scoped>
    h3 {
        margin-bottom:5px;
    }

    form {
        display:flex;
    }

    form input {
        border:none;
        outline:none;

        background-color:var(--color-bg-secondary);
        color:var(--color-main);

        font-family:inherit;
        font-size:1.1rem;

        padding:15px;
        border-top-left-radius:10px;
        border-bottom-left-radius:10px;

        width:100%;
    }

    form button {
        border:none;
        outline:none;

        background-color:var(--color-accent);
        color:var(--color-main);

        font-family:inherit;
        font-size:1.1rem;

        padding:0px 15px;
        border-top-right-radius:10px;
        border-bottom-right-radius:10px;

        transition-duration:0.2s;
    }
    form button:hover {
        background-color:var(--color-accent-hover);
        cursor:pointer;
    }
</style>
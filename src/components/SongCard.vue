<template>
    <div>
        <img :src="imgUrl" :alt="songTitle">
        <h5>{{ songTitle }}</h5>
        <p>{{ author }}</p>
        <p>{{ year }}</p>
    </div>
</template>

<script>
export default {
    props:{
        imgUrl: String,
        songTitle: String,
        author: String,
        year: String
    }
}
</script>

<style lang="scss" scoped>
    div{
        background: #2e3a46;
        height: 100%;
        margin: 0.5rem 0;
        padding: 1rem;

        img{
            width: 100%;
        }

        h5{
            color: whitesmoke;
            text-transform: uppercase;
            padding: 1rem 0;
        }

        p{
            color: #6a7176;
            margin: 0;
            padding: 0;
        }
    }
</style>
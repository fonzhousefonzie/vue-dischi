<template>
    <header class="px-3 d-flex justify-content-between">
        <img alt="Spotify Logo" src="https://grafica-facile.com/wp-content/uploads/2022/01/spotify-logo.png">
    </header>
</template>

<script>
export default {
    
}
</script>

<style lang="scss" scoped>
    header{
        background: #2e3a46;
        max-height: 50px;
        padding: 0.5rem 1rem;

        img{
            max-height: calc(50px - 1rem);
        }

        .search-bar{
            display: flex;
            gap: 0.5rem;
            color: white;
            align-items: center;
        }
    }
</style>
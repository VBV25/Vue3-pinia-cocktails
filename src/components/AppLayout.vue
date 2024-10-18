<template>
    <div class="root">
        <div class="img" :style="`background-image: url(${imgUrl})`">

        </div>
        <div class="main">
            <el-button class="btn">Get random cocktail</el-button>
        </div>
    </div>
</template>

<script setup>
const props = defineProps({
    imgUrl: {
        type: String,
        required: true
    }
})
</script>

<style lang="scss" scoped>
@use '../assets/styles/main' as *;

.root {
    min-height: 100vh;
    display: flex;
    background-color: $background;
}

.img{
width: 50%;

background-repeat: no-repeat;
background-position: 50% 50%;
background-size: cover;
}

.main{
    width: 50%;
}

</style>
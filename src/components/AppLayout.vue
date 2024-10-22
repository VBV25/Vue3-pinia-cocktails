<template>
    <div class="root">
        <div class="img" :style="`background-image: url(${imgUrl})`">

        </div>
        <div class="main">
            <el-button class="btn">Get random cocktail</el-button>
            <slot></slot>
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

.img {
    left: 0px;
    top: 0px;
    width: 50%;

    background-repeat: no-repeat;
    background-position: start start;
    background-size: 100% 100vh;
}

.main {
    position: relative;
    width: 50%;
    padding: 32px 40px;
}

.btn {
    position: absolute;
    top: 32px;
    right: 40px;

    background-color: $accent;
    border: unset;

    font-family: $fontBase;
    font-size: 16px;
    color: $text;

    &:hover,
    &:active {
        background-color: darken($accent, 15%);
    }
}
</style>
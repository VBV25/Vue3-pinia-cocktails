<template>
    <div class="root">
        <div class="img" :style="`background-image: url(${imgUrl})`"></div>
        <div class="main">
            <div class="btns">
                <el-button v-if="isBackButtonVisible" type="primary" :icon="Back" circle class="back"
                    @click="goBack" />
                <el-button class="btn" @click="goForCocktailRandom">Get random cocktail</el-button>
            </div>
            <slot></slot>
        </div>
    </div>
</template>

<script setup>
import { useRoute, useRouter } from 'vue-router';
import { Back } from '@element-plus/icons-vue'
import { computed } from 'vue';
import { ROUTES_PATH } from '@/constants'

const props = defineProps({
    imgUrl: {
        type: String,
        required: true
    },
    backFunc: {
        type: Function
    },
    isBackButtonVisible: {
        type: Boolean,
        default: true
    },
})

const route = useRoute()
const router = useRouter()

const routName = computed(() => route.name)

function goForCocktailRandom(){
    router.push(ROUTES_PATH.COCKTAIL_RANDOM)

    if(routName.value === ROUTES_PATH.COCKTAIL_RANDOM){
        router.go()
    }
}

function goBack(){
    props.backFunc ? props.backFunc() : router.go(-1)
}

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

.btns {
    display: flex;
    justify-content: space-between;
    align-items: center;
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

.back {
    background-color: transparent;
    border-color: #fff;

    &:hover {
        border-color: $accent;
    }
}
</style>
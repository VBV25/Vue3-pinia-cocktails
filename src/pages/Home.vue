<template>
    <AppLayout imgUrl="./src/assets/img/dawa-cocktail.png">
        <div class="wrapper">
            <div v-if="!ingredient || !cocktails" class="info">
                <h2 class="title">Choose your drink</h2>
                <div class="line"></div>
                <div class="select-wrapper">
                    <el-select v-model="ingredient" placeholder="Chose your drink" size="large" class="select"
                        @change="getCocktails">
                        <el-option v-for="item in ingredients" :key="item.strIngredient1" :label="item.strIngredient1"
                            :value="item.strIngredient1" />
                    </el-select>
                </div>
                <div class="text">Try our delicious cocktail recipes for every occasion. Find delicious cocktail recipes
                    by ingredient through our cocktail generator.</div>
                <img src="/src/assets/img/cocktails-list.png" class="cocktails-img" alt="cocktails-img">
            </div>

            <div v-else class="info">
                <h2 class="title">COCKTAILS WITH {{ ingredient }}</h2>
                <div class="line"></div>
                <div class="cocktails">
                    <CocktailThumb v-for="cocktail in cocktails" :key="cocktail.idDrink" :cocktailData="cocktail">
                    </CocktailThumb>
                </div>
            </div>
        </div>
    </AppLayout>
</template>

<script setup>
// Food_Drink.png

import { ref } from 'vue';
import { useRootStore } from '@/stores/root';
import { storeToRefs } from 'pinia'

import AppLayout from '@/components/AppLayout.vue';
import CocktailThumb from '@/components/CocktailThumb.vue';


const rootStore = useRootStore()
rootStore.getIngredients()

const { ingredients, cocktails } = storeToRefs(rootStore)
const ingredient = ref(null)

function getCocktails() {
    rootStore.getCocktails(ingredient.value)
}
</script>

<style lang="scss" scoped>
@use '../assets/styles/main' as *;

.wrapper {
    display: flex;
    justify-content: center;
    align-items: center;
}

.info {
    width: 100%;
    padding: 60px 0px 0px;
    text-align: center;
}

.select-wrapper {
    padding-top: 50px;
}

.select {
    width: 220px;
}

.text {
    max-width: 516px;
    padding-top: 50px;
    margin: 0 auto;

    line-height: 36px;
    letter-spacing: 0.1em;
    color: $textMuted;
}

.cocktails-img {
    max-width: 100%;
    margin-top: 60px;
}

.cocktails {
    width: 100%;
    max-height: 70vh;
    margin-top: 32px;
    overflow-y: scroll;
    overflow-x: hidden;

    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    row-gap: 36px;

    &::-webkit-scrollbar {
        width: 3px;
    }

    &::-webkit-scrollbar-track {
        border-radius: 10px;
        background: $background;
    }

    &::-webkit-scrollbar-thumb {
        background-color: $accent;
        border-radius: 10px;
    }
}
</style>
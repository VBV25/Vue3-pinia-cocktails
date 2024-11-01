<template>
    <div v-if="cocktail" class="wrap">
        <AppLayout :imgUrl="cocktail.strDrinkThumb">
            <div class="wrapper">
                <div class="info">
                    <h2 class="title">{{ cocktail.strDrink }}</h2>
                    <div class="line"></div>
                    <div class="slider">
                        <swiper :modules="modules" :slides-per-view="3" :space-between="50" class="swiper"
                            :scrollbar="{ draggable: true }">
                            <swiper-slide v-for="(ingredient, key) in ingredients" :key="key">
                                <div class="ingredient">
                                    <img :src="`${INGREDIENT_PIC}${ingredient.name}-Small.png`"
                                        alt="INGREDIENT" class="ingredient-img">
                                    <div class="ingredient-name"> {{ ingredient.name }}</div>
                                    <div class="ingredient-line"></div>
                                    <div class="ingredient-measure"> {{ ingredient.measure ? ingredient.measure : '-' }}</div>

                                </div>
                            </swiper-slide>
                        </swiper>
                    </div>
                    <div class="instructions">{{ cocktail.strInstructions }}</div>
                </div>
            </div>
        </AppLayout>
    </div>
</template>

<script setup>
import axios from 'axios';
import { ref, computed } from 'vue';

import { Swiper, SwiperSlide } from 'swiper/vue';
import { Scrollbar } from 'swiper/modules';
import 'swiper/css';
import 'swiper/css/scrollbar';

import { COCKTAIL_RANDOM, INGREDIENT_PIC } from '@/constants'
import AppLayout from '@/components/AppLayout.vue';

const modules = [Scrollbar]
const cocktail = ref(null)

const ingredients = computed(() => {
    const ingredients = []
    for (let i = 1; i <= 15; i++) {
        if (!cocktail.value[`strIngredient${i}`]) break      
        const ingredient = {}
        ingredient.name = cocktail.value[`strIngredient${i}`]
        ingredient.measure = cocktail.value[`strMeasure${i}`]
        ingredients.push(ingredient)
    }
    return ingredients
})

async function getCocktail() {
    const data = await axios.get(COCKTAIL_RANDOM)
    cocktail.value = data?.data?.drinks[0]
}

getCocktail()
</script>

<style lang="scss" scoped>
@use '../assets/styles/main' as *;

.slider {
    margin: 50px 0px;
}

.swiper {
    cursor: grab;
    width: 100%;
    padding-bottom: 25px;

    &:active{
        cursor:grabbing;
    }
}

.ingredient {
    display: flex;
    flex-direction: column;
    align-items: center;

    &-img {
        width: 100px;
        height: 100px;
        margin-bottom: 15px;
    }

    &-name{
        width: 100%;
        white-space: nowrap;
        overflow: hidden;
        text-overflow: ellipsis;
    }

    &-line{
        width: 20%;
        height: 1px;
        background-color: $accent;
        margin: 3px 0px;
    }
}
</style>
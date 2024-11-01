<template>
    <div class="root">
        <RouterLink :to="`/cocktails/${cocktailData.idDrink}`" class="cocktail-card">
            <div class="img" :style="`background-image: url(${cocktailData.strDrinkThumb})`"> </div>
            <div class="name"> {{ cocktailData.strDrink }} </div>
        </RouterLink>

    </div>
</template>

<script setup>
const props = defineProps({
    cocktailData: {
        type: Object,
        required: true
    }
})
</script>

<style lang="scss" scoped>
@use '../assets/styles/main' as *;

.root {
    cursor: pointer;
    width: calc(100% / 3);
    padding: 0px 10px;

    display: flex;
    flex-direction: column;
    align-items: center;
}

.cocktail-card {
    display: flex;
    flex-direction: column;
    align-items: center;
}

.img {
    width: 120px;
    height: 120px;
    
    background-repeat: no-repeat;
    background-position: 50% 50%;
    background-size: cover;
}

.name {
    padding-top: 15px;
    letter-spacing: 0.1em;
}
</style>
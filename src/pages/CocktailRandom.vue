<script setup>
import axios from 'axios';
import { computed, ref } from 'vue';
import { COCKTAIL_RANDOM, INGREDIENT_PIC } from '@/constants';
import AppLayout from '../components/AppLayout.vue';
import { Swiper, SwiperSlide } from 'swiper/vue';
import 'swiper/css';

const ingredients = computed(() => {
  const ingredients = [];

  for (let i = 1; i <= 15; i++) {
    if (!cocktail.value[`strIngredient${i}`]) break;
    const ingredient = cocktail.value[`strIngredient${i}`];

    ingredients.push(ingredient);
  }

  return ingredients;
});

const cocktail = ref(null);

async function getCocktail() {
  const data = await axios.get(COCKTAIL_RANDOM);
  cocktail.value = data?.data?.drinks[0];
}

getCocktail();
</script>

<template v-if="cocktail">
  <AppLayout :imgUrl="cocktail.strDrinkThumb">
    <div class="wrapper">
      <div v-if="!ingredient || !cocktails" class="info">
        <h1 class="title">{{ cocktail.strDrink }}</h1>
        <div class="line"></div>
        <div :class="$style.slider">
          <swiper
            :class="$style.swiper"
            :slides-per-view="3"
            :space-between="50"
          >
            <swiper-slide
              v-for="(ingredient, key) in ingredients"
              :key="key"
              :class="$style.slide"
            >
              <img
                :src="`${INGREDIENT_PIC}${ingredient}-Small.png`"
                :alt="ingredient"
                :class="$style.img"
              />
              <p :class="$style.name">{{ ingredient }}</p></swiper-slide
            >
          </swiper>
        </div>
        <p :class="$style.instruction">{{ cocktail.strInstructions }}</p>
      </div>
    </div>
  </AppLayout>
</template>

<style module lang="scss">
.instruction {
  width: 100%;
  text-align: center;
  color: var(--color-text-muted);
  font-size: 1.4rem;
  line-height: 2.6rem;
  letter-spacing: 0.2rem;
}

.list {
  color: var(--color-text);
  font-size: 1.2rem;
  line-height: 2.4rem;
  letter-spacing: 0.2rem;
  margin-bottom: 3rem;
  list-style: url('../assets/img/heart.png');
}

.item {
  padding-left: 1rem;

  &:not(:last-child) {
    margin-bottom: 1rem;
  }
}

.slider {
  margin-bottom: 3rem;
}

.swiper {
  width: 650px;
}

.slide {
  display: flex;
  flex-flow: column wrap;
  width: 100px;
  align-items: center;
}

.img {
  height: 79px;
  width: 100%;
  margin-bottom: 1rem;
  object-fit: contain;
}

.name {
  width: 100%;
  font-family: 'Raleway', 'Arial', sans-serif;
  font-weight: 500;
  letter-spacing: 2px;
  text-align: center;
  font-size: 1rem;
}
</style>

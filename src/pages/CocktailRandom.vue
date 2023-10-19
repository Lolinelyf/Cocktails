<script setup>
import axios from 'axios';
import { computed, ref } from 'vue';
import { useRoute, useRouter } from 'vue-router';
import { COCKTAIL_RANDOM } from '@/constants';
import AppLayout from '../components/AppLayout.vue';
import { Swiper, SwiperSlide } from 'swiper/vue';
import 'swiper/css';

const route = useRoute();
const router = useRouter();
const cocktailId = computed(() => route.path.split('/').pop());
const ingredients = computed(() => {
  const ingredients = [];

  for (let i = 1; i <= 15; i++) {
    if (!cocktail.value[`strIngredient${i}`]) break;
    const ingredient = {};

    ingredient.name = cocktail.value[`strIngredient${i}`];
    ingredient.measure = cocktail.value[`strMeasure${i}`];

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

function goBack() {
  router.go(-1);
}
</script>

<template v-if="cocktail">
  <AppLayout :imgUrl="cocktail.strDrinkThumb" :backFunk="goBack">
    <div class="wrapper">
      <div v-if="!ingredient || !cocktails" class="info">
        <h1 class="title">{{ cocktail.strDrink }}</h1>
        <div class="line"></div>
        <div :class="$style.slider">
          <swiper
            :class="$style.swiper"
            :slides-per-view="1"
            :space-between="50"
          >
            <swiper-slide>Slide 1</swiper-slide>
            <swiper-slide>Slide 2</swiper-slide>
            <swiper-slide>Slide 3</swiper-slide>
            ...
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
</style>

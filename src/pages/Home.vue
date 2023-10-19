<script setup>
import AppLayout from '../components/AppLayout.vue';
import { useRootStore } from '../stores/root';
import { storeToRefs } from 'pinia';
import CocktailPage from '../components/CocktailPage.vue';

const rootStore = useRootStore();
rootStore.getIngredients();

const { ingredients, ingredient, cocktails } = storeToRefs(rootStore);

function getCocktails() {
  rootStore.getCocktails(rootStore.ingredient);
}

function removeIngredient() {
  rootStore.setIngredient(null);
}
</script>

<template>
  <AppLayout
    imgUrl="/src/assets/img/bg-1.jpg"
    :backFunk="removeIngredient"
    :is-back-button-visible="!!ingredient"
  >
    <div class="wrapper">
      <div v-if="!ingredient || !cocktails" class="info">
        <h1 class="title">Choose your drink</h1>
        <div class="line"></div>
        <div :class="$style.selected">
          <el-select
            v-model="rootStore.ingredient"
            placeholder="Choose main ingredient"
            size="large"
            filterable
            allow-create
            class="select"
            @change="getCocktails"
          >
            <el-option
              v-for="item in ingredients"
              :key="item.strIngredient1"
              :label="item.strIngredient1"
              :value="item.strIngredient1"
            />
          </el-select>
        </div>
        <div :class="$style.text">
          Try our delicious cocktail recipes for every occasion. Find delicious
          cocktail recipes by ingredient through our cocktail generator.
        </div>
        <img :class="$style.img" src="/src/assets/img/cocktails.png" alt="" />
      </div>

      <div v-else class="info">
        <h1 class="title">COCKTAILS WITH Midori melon liqueur</h1>
        <div class="line"></div>
        <div :class="$style.cocktails">
          <CocktailPage
            v-for="cocktail in cocktails"
            :key="cocktail.idDrink"
            :cocktail="cocktail"
            :class="$style.cocktail"
          />
        </div>
      </div>
    </div>
  </AppLayout>
</template>

<style module lang="scss">
.selected {
  padding-bottom: 3rem;
}

.text {
  width: 516px;
  text-align: center;
  font-size: 1rem;
  font-weight: 400;
  padding-bottom: 3rem;
  letter-spacing: 0.1rem;
  line-height: 2rem;
  color: var(--color-text-muted);
}

.cocktails {
  display: flex;
  width: 100%;
  flex-flow: row wrap;
  gap: 3rem;
  overflow-y: auto;
  height: 700px;

  &::-webkit-scrollbar {
    width: 0;
  }
}
</style>

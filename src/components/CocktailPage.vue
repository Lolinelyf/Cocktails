<script setup>
const props = defineProps({
  cocktail: {
    type: Object,
    required: true,
  },
});
</script>
<template>
  <div :class="$style.root">
    <RouterLink :to="`/cocktails/${cocktail.idDrink}`">
      <div
        :style="`background-image: url(${cocktail.strDrinkThumb})`"
        :class="$style.pic"
      ></div>
      <p :class="$style.name">{{ cocktail.strDrink }}</p>
    </RouterLink>
  </div>
</template>
<style module>
.root {
  width: calc((100% - 6rem) / 3);
}

.pic {
  width: 100%;
  height: 176px;
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
  margin-bottom: 1rem;
}

.name {
  margin: 0;
  padding: 0;
  font-family: 'Raleway', 'Arial', sans-serif;
  letter-spacing: 2px;
  font-weight: 400;
}
</style>

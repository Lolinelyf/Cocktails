<script setup>
const props = defineProps({
  imgUrl: {
    type: String,
    required: true,
  },
});
</script>

<template>
  <div :class="$style.root">
    <div :style="`background-img: url(${imgUrl});`" :class="$style.img"></div>
    <div :class="$style.main">
      <el-button :class="$style.button">Get random cocktail</el-button>
    </div>
  </div>
</template>

<style module lang="scss">
.root {
  display: flex;
  min-height: 100vh;
  background-color: var(--color-background);
}

.img {
  width: 50%;
  background-repeat: no-repeat;
  background-position: 50% 50%;
  background-size: cover;
}

.main {
  position: relative;
  width: 500%;
  padding: 2rem 2.2rem;
}

.button {
  position: absolute;
  top: 2rem;
  right: 2.2rem;
  font-family: 'Raleway', 'Arial', sans-serif;
  background-color: var(--color-accent);
  border-color: var(--color-accent);
  color: var(--color-text);
  transition: opacity 0.15s;

  &:hover {
    background-color: var(--color-accent);
    border-color: var(--color-accent);
    color: var(--color-text);
    opacity: 0.8;
  }
  &:active {
    background-color: var(--color-accent);
    border-color: var(--color-accent);
    color: var(--color-text);
    opacity: 0.6;
  }
}
</style>

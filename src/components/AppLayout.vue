<script setup>
import { useRoute, useRouter } from 'vue-router';
import { Back } from '@element-plus/icons-vue';
import { computed } from 'vue';
import { ROUTES_PATH } from '@/constants';

const props = defineProps({
  imgUrl: {
    type: String,
    required: true,
  },
  backFunk: {
    type: Function,
    required: true,
  },
  isBackButtonVisible: {
    type: Boolean,
    default: true,
  },
});

const route = useRoute();
const router = useRouter();
const routeName = computed(() => route.name);

function goForCocktailRandom() {
  router.push(ROUTES_PATH.COCKTAIL_RANDOM);

  if (routeName.value === ROUTES_PATH.COCKTAIL_RANDOM) {
    router.go();
  }
}
</script>

<template>
  <div :class="$style.root">
    <div :style="`background-image: url(${imgUrl});`" :class="$style.img"></div>
    <div :class="$style.main">
      <div :class="$style.btns">
        <el-button
          v-if="isBackButtonVisible"
          :class="$style.back"
          type="primary"
          :icon="Back"
          circle
          @click="backFunk"
        />
        <el-button :class="$style.button" @click="goForCocktailRandom"
          >Get random cocktail</el-button
        >
      </div>

      <slot></slot>
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
  width: 45%;
  height: 100vh;
  background-repeat: no-repeat;
  background-position: center;
  background-size: cover;
}

.main {
  position: relative;
  width: 55%;
  padding: 2rem 2.2rem;
}

.button {
  position: absolute;
  top: 2rem;
  right: 2.2rem;
  padding: 1rem;
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

.btns {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.back {
  background-color: inherit;
  border-color: var(--color-text);
  padding: 1rem;
  transition: background-color 0.15s border-color 0.15s;

  &:hover {
    background-color: #ffffff15;
    border-color: var(--color-text);
  }
  &:active {
    background-color: #ffffff21;
    border-color: var(--color-text);
  }
}
</style>

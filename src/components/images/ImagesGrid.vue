<script setup>
import { computed } from 'vue';

const COLUMNS = 2;

const props = defineProps({
  images: {
    type: Array,
    required: true,
  },
});

const columns = computed(() => {
  const result = [];

  for (let i = 0; i < COLUMNS; i++) {
    result.push(props.images.filter((_, index) => index % COLUMNS === i));
  }

  return result;
});
</script>

<template>
  <section class="images-grid">
    <div v-for="(column, i) in columns" :key="i" class="images-grid__column">
      <img v-for="img in column" :key="img" :src="img.pic" alt="" />
    </div>
  </section>
</template>

<style lang="scss" scoped>
.images-grid {
  height: 100%;
  width: 100%;
  display: grid;
  grid-template-columns: repeat(v-bind(COLUMNS), 1fr);

  &__column {
    display: flex;
    flex-direction: column;
    width: 100%;

    img {
      width: 100%;
      height: auto;
    }
  }
}
</style>

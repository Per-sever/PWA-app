<template>
  <section class="images-list">
    <div v-for="img in images" :key="img" class="images-list__item">
      <img class="images-list__img" :src="img.pic" alt="" />
      <div :src="str" class="images-list__info">
        {{ img.description }}
      </div>
    </div>
  </section>
</template>

<script setup>
defineProps({
  images: {
    type: Array,
    required: true,
  },
});
</script>

<style lang="scss" scoped>
.images-list {
  display: flex;
  width: 100%;
  flex-direction: column;

  &__item {
    display: flex;
    height: 10rem;
    margin-bottom: 1rem;
    border: 0.1rem solid #000;
    padding: 0.5rem;
    position: relative;
    overflow: hidden;
    flex-shrink: 0;
  }

  &__img {
    width: auto;
    height: 100%;
    margin-right: 1rem;
  }
}
</style>

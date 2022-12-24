<script setup>
defineProps({
  modelValue: {
    type: String,
    default: '',
  },
});

const emit = defineEmits(['update:modelValue']);

const handleInput = (event) => {
  emit('update:modelValue', event.target.value);
};
</script>

<template>
  <div class="search-bar">
    <img :src="searchImg" alt="" class="search-bar__img" />
    <input
      :value="modelValue"
      class="search-bar__input"
      placeholder="🔎Введите название статьи"
      @input="handleInput"
    />
  </div>
</template>

<style lang="scss" scoped>
.search-bar {
  display: flex;
  align-items: center;
  background: ghostwhite;
  border-radius: 0.4rem;
  padding: 0 0.5rem;

  &__img {
    width: 1rem;
    height: auto;
    margin-right: 0.5rem;
  }

  &__input {
    height: 3rem;
    flex-grow: 2;
    background: transparent;
    font-weight: 700;
    &:focus {
      outline: none;
    }
  }
}
</style>

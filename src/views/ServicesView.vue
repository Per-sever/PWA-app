<script setup>
import { computed, ref } from 'vue';

const services = [
  {
    id: 0,
    title: 'Веб разработка',
    price: 300,
  },
  {
    id: 1,
    title: 'Дизайн',
    price: 400,
  },
  {
    id: 2,
    title: 'Интеграция',
    price: 250,
  },
  {
    id: 3,
    title: 'Обучение',
    price: 220,
  },
];

const chosenServices = ref([]);

const checkedServices = computed(() =>
  services.map((service) => {
    const chosenService = chosenServices.value.includes(service.id);
    return { ...service, chosenService };
  })
);

const result = computed(() =>
  checkedServices.value.reduce(
    (acc, service) => (service.chosenService ? acc + service.price : acc),
    0
  )
);

const handleServiceClick = (service) => {
  if (service.chosenService) {
    chosenServices.value = chosenServices.value.filter(
      (id) => id !== service.id
    );
    return;
  }
  chosenServices.value.push(service.id);
};
</script>

<template>
  <section class="services-view">
    <h2 class="services-view__title">Услуги</h2>

    <div class="services-view__content">
      <div class="services-view__list">
        <div
          v-for="service in checkedServices"
          :key="service.id"
          class="services-view__item"
          :class="{ 'services-view__item--chosen': service.chosenService }"
          @click="handleServiceClick(service)"
        >
          <div class="services-view__item-title">
            {{ service.title }}
          </div>

          <div class="services-view__item-description">
            {{ service.description }}
          </div>

          <hr />
          <div class="services-view__item-price">${{ service.price }}.00</div>
        </div>
      </div>

      <div class="services-view__result">
        <span>Сумма:</span>
        <span>${{ result }}.00 </span>
      </div>
    </div>
  </section>
</template>

<style lang="scss" scoped>
.services-view {
  position: relative;
  background: grey;
  display: flex;
  flex-direction: column;
  align-items: center;
  height: 100%;
  padding-top: 1rem;
  background: #5aa3ba;

  &__title {
    padding: 35 px;
    padding-bottom: 35px;
    color: #fff;
    font-size: 4rem;
    font-weight: bold;
  }

  &__content {
    padding: 1rem 0;
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  &__list {
    padding: 0 5% 1rem 5%;
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    width: 80%;
    overflow: auto;

    @include layout-mobile {
      padding: 0 5% 1rem 5%;
    }

    &::-webkit-scrollbar {
      width: 0.5rem;
    }

    &::-webkit-scrollbar-track {
      background: transparent;
    }

    &::-webkit-scrollbar-thumb {
      background: #a7a5a5;
      border-radius: 0.5rem;
    }
  }

  &__item {
    user-select: none;
    cursor: pointer;
    display: flex;
    padding: 1rem;
    justify-content: space-between;
    align-items: center;
    background: white;
    border-radius: 0.2rem;
    color: white;
    background: #e75684;
    font-size: 1rem;
    font-weight: bold;
    transition: color 0.2s ease-in-out, background 0.2s ease-in-out;

    &:hover {
      filter: brightness(1.1);
      opacity: 0.8;
    }

    &--chosen {
      background: #8ebf74;
    }

    & + & {
      margin-top: 0.5rem;
    }
  }

  &__item-price {
    font-size: 1.2rem;
    font-weight: bold;
  }

  &__result {
    border-top: 1px white solid;
    font-size: 1.2rem;
    font-weight: bold;
    align-items: center;
    display: flex;
    justify-content: space-between;
    color: white;
    width: 100%;
    padding: 1rem 8rem;

    @include layout-mobile {
      padding: 1rem 5%;
    }
  }
}
</style>

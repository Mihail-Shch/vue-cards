<template>
  <div class="card">
    <img src="@/assets/img/card-photo.png" alt="card photo" />
    <div class="card__info">
      <h3 class="card__info-title">{{ card.name }}</h3>
      <p class="card__info-desc">{{ card.description }}</p>
      <span class="card__info-price">{{ card.price }} руб.</span>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    card: Object,
  },
};
</script>

<style lang="scss" scoped>
</style>
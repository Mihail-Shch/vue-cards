<template>
  <div class="card" @mouseover="hover = true" @mouseleave="hover = false">
    <img
      :src="card.path"
      class="card__photo"
      alt="card photo"
      crossorigin="anonymous"
    />
    <div class="card__info">
      <div class="card__info-text">
        <h3 class="card__info-title">{{ card.name }}</h3>
        <p class="card__info-desc">{{ card.description }}</p>
      </div>
      <span class="card__info-price">{{ card.price }} руб.</span>
    </div>
    <transition name="fade">
      <div v-if="hover" class="card__delete" @click="$emit('delete', card)">
        <img src="@/assets/img/trash.svg" alt="trash" />
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  data() {
    return {
      hover: false,
    };
  },
  props: {
    card: Object,
  },
};
</script>

<style lang="scss" scoped>
.card {
  @extend %column;
  position: relative;
  cursor: pointer;

  &__photo {
    height: 100%;
    max-width: 100%;
    border-radius: $cardBorderRadius $cardBorderRadius 0 0;
  }

  &__info {
    height: 100%;
    background-color: $white;
    border-radius: 0 0 $cardBorderRadius $cardBorderRadius;

    padding: $cardInfoPadding;

    @extend %column;
    justify-content: space-between;

    &-title {
      font-size: $cardTitleFontSize;
      margin-bottom: 16px;
    }

    &-desc {
      font-size: $cardDescFontSize;
      font-weight: 300;

      margin-bottom: 32px;
    }

    &-price {
      font-size: $cardPriceFontSize;
    }
  }
  &__delete {
    @extend %center;
    width: $cardDeleteWidth;
    height: $cardDeleteHeigth;
    border-radius: $cardDeleteRadius;
    background-color: $pink;

    position: absolute;
    top: calc($cardDeleteHeigth / -4);
    right: calc($cardDeleteWidth / -4);

    &:hover {
      background-color: $darkPink;
    }
  }
}

// animation classes

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease-in-out;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}
</style>
<template>
  <div class="card" @mouseover="hover = true" @mouseleave="hover = false">
    <div class="card__inner">
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
  position: relative;
  box-shadow: $cardBoxShadow;
  border-radius: $cardBorderRadius;
  cursor: pointer;

  &__inner {
    @extend %column;
    overflow: hidden;
    border-radius: inherit;
  }

  &__photo {
    max-width: 100%;
  }

  &__info {
    height: 100%;
    background-color: $white;

    padding: $cardInfoPadding;

    @extend %column;
    justify-content: space-between;

    &-title {
      font-size: $cardTitleFontSize;
      font-weight: 600;
      margin-bottom: 16px;
    }

    &-desc {
      font-size: $cardDescFontSize;
      line-height: 1.25;

      margin-bottom: 32px;
    }

    &-price {
      font-size: $cardPriceFontSize;
      font-weight: 600;
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
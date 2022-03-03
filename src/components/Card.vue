<template>
  <div class="card" @mouseover="hoverOver" @mouseleave="hoverOut">
    <img src="@/assets/img/card-photo.png" alt="card photo" />
    <div class="card__info">
      <h3 class="card__info-title">{{ card.name }}</h3>
      <p class="card__info-desc">{{ card.description }}</p>
      <span class="card__info-price">{{ card.price }} руб.</span>
    </div>
    <div class="card__delete" :class="trashClasses" v-if="hover">
      <img src="@/assets/img/trash.svg" alt="trash" />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      hover: false,
      trashClasses: [],
    };
  },
  methods: {
    hoverOver() {
      this.trashClasses = ["fadeIn"];
      this.hover = true;
    },
    hoverOut() {
      this.trashClasses = ["fadeOut"];
      setTimeout(() => {
        this.hover = false;
      }, 300);
    },
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
  &__info {
    background-color: $white;
    padding: $cardInfoPadding;

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

    transition: $transition;

    opacity: 0;

    &.fadeIn {
      animation: fadeIn 0.3s ease-in-out forwards;
    }

    &.fadeOut {
      animation: fadeOut 0.3s ease-in-out forwards;
    }

    &:hover {
      background-color: $darkPink;
    }
  }
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

@keyframes fadeOut {
  from {
    opacity: 1;
  }
  to {
    opacity: 0;
  }
}
</style>
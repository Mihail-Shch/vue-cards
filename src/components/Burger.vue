<template>
  <div
    :class="['header__burger', { active: isActive }]"
    @click="$emit('toggle', (isActive = !isActive))"
  >
    <span class="header__burger-span"> </span>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isActive: false,
    };
  },
};
</script>

<style lang="scss" scoped>
.header__burger {
  width: $headerBurgerWidth;
  height: $headerBurgerHeight;

  border: 1px solid #000;
  border-radius: 50%;
  @extend %center;

  display: none;

  &:hover {
    cursor: pointer;
  }

  &-span {
    display: inline-block;
    width: 28px;
    height: 2px;
    background-color: $black;

    position: relative;

    &::before,
    &::after {
      display: block;
      content: "";
      width: 100%;
      height: 100%;
      background-color: $black;

      position: absolute;
      left: 0;
      transition: transform 0.2s ease-in, top 0.2s linear 0.2s;
    }

    &::before {
      top: -8px;
    }

    &::after {
      top: 8px;
    }
  }
  &.active &-span {
    background-color: transparent;
  }

  &.active &-span::before {
    transform: rotate(45deg);
    top: 0;
    transition: top 0.2s linear, transform 0.2s ease-in 0.2s;
  }

  &.active &-span::after {
    transform: rotate(-45deg);
    top: 0;
    transition: top 0.2s linear, transform 0.2s ease-in 0.2s;
  }
}

@media (max-width: 1070px) {
  .header__burger {
    display: flex;
  }
}
</style>
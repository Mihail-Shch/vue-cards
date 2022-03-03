<template>
  <div
    class="filters"
    @click="isActive = !isActive"
    v-click-outside="closeFilters"
  >
    <p class="filters__title">
      {{ selected }}
      <img class="filters__arrow" src="@/assets/img/arrow.svg" alt="arrow" />
    </p>
    <div class="filters__options" v-if="isActive">
      <p
        class="filter"
        v-for="option in options"
        :key="option.value"
        @click="selected = option.name"
      >
        {{ option.name }}
      </p>
    </div>
  </div>
</template>

<script>
import ClickOutside from "vue-click-outside";
export default {
  data() {
    return {
      selected: "",
      isActive: false,
    };
  },
  props: {
    options: Array,
  },
  methods: {
    closeFilters() {
      this.isActive = false;
    },
  },
  created() {
    this.selected = this.options[0].name;
  },
  directives: {
    ClickOutside,
  },
};
</script>

<style lang="scss" scoped>
.filters {
  color: $grey;
  font-size: $filterFontSize;
  font-weight: 300;

  background-color: $white;
  border-radius: $filtersBorderRadius;

  padding: $filtersPadding;

  box-shadow: $filtersShadow;

  cursor: pointer;

  position: relative;

  &__arrow {
    margin-left: 5px;
  }

  &__options {
    background-color: $white;
    border-radius: $filtersBorderRadius;

    width: 100%;
    text-align: center;

    position: absolute;
    top: 40px;
    left: 0;

    .filter {
      padding: 10px 0;
      transition: background-color 0.2s linear;

      &:hover {
        background-color: rgb(233, 231, 231);
      }
    }
  }
}
</style>
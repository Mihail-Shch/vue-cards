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
      <li
        class="filter"
        v-for="option in filters"
        :key="option.value"
        @click="setFilteredCards(option)"
      >
        {{ option.name }}
      </li>
    </div>
  </div>
</template>

<script>
import ClickOutside from "vue-click-outside";
import axios from "axios";
export default {
  data() {
    return {
      selected: "",
      isActive: false,
    };
  },
  props: {
    filters: Array,
    value: Array,
  },
  watch: {
    value(val) {
      this.cardsCopy = val;
    },
  },
  methods: {
    closeFilters() {
      this.isActive = false;
    },
    async setFilteredCards(option) {
      this.selected = option.name;

      const req = await axios.get(
        `http://localhost:3000/api/sortCards?q=${option.value}`
      );
      console.log(req);
      this.$emit("input", req.data);
    },
  },
  created() {
    this.selected = this.filters[0].name;
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

  background-color: $white;
  border-radius: $filtersBorderRadius;

  padding: $filtersPadding;

  box-shadow: $filtersBoxShadow;

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
    z-index: 2;

    .filter {
      padding: $filterPadding;
      transition: $transition;
      list-style-type: none;

      &:hover {
        background-color: $lightGrey;
      }
    }
  }
}
</style>
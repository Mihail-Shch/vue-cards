<template>
  <button :class="[{ disabled: disabled, enabled: enabled }]">
    <slot />
  </button>
</template>

<script>
export default {
  props: {
    disabled: Boolean,
    enabled: Boolean,
  },
};
</script>

<style lang="scss" scoped>
button {
  width: 100%;
  padding: $btnPadding;
  color: $grey;

  border-radius: $btnBorderRadius;

  transition: background-color 0.2s linear;
}

.disabled {
  pointer-events: none;
}

.enabled {
  color: $white;
  background-color: $green;
}

button.enabled:hover {
  background-color: $darkGreen;
}
</style>
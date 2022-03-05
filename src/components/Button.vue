<template>
  <button>
    <slot />
  </button>
</template>

<style lang="scss" scoped>
button {
  width: 100%;
  padding: $btnPadding;
  color: $grey;
  font-weight: 600;

  border-radius: $btnBorderRadius;

  transition: $transition;
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
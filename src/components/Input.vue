<template>
  <textarea
    v-if="textarea"
    @input="$emit('input', $event.target.value)"
  ></textarea>
  <input v-else type="text" @input="$emit('input', $event.target.value)" />
</template>

<script>
export default {
  props: {
    textarea: Boolean,
  },
};
</script>

<style lang="scss" scoped>
input,
textarea {
  width: 100%;
  font-size: $inputFontSize;

  border: 1px solid transparent;
  border-radius: $inputBorderRadius;

  padding: $inputPadding;
  box-shadow: $inputBoxShadow;

  resize: none;

  &:focus {
    background: $ligthBlue;
    border: 1px solid $blue;
  }
}
</style>
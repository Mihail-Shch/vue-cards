<template>
  <textarea
    v-if="textarea"
    v-model="content"
    @input="emit('input', content)"
  ></textarea>
  <input v-else v-model="content" @input="$emit('input', content)" />
</template>

<script>
export default {
  data() {
    return {
      content: "",
    };
  },
  props: {
    value: [String, Number],
    textarea: Boolean,
  },
  watch: {
    value(val) {
      this.content = val;
    },
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
    background: $lightBlue;
    border: 1px solid $blue;
  }
}
</style>
<template>
  <form class="form">
    <span class="form__input-title required">Наименование товара</span>
    <Input class="form__input" placeholder="Введите наименование товара" />
    <span class="form__input-title">Описание товара</span>
    <Input
      class="form__input"
      placeholder="Введите описание товара"
      rows="6"
      textarea
    />
    <span class="form__input-title required">Ссылка на изображение товара</span>
    <Input class="form__input" placeholder="Введите ссылку" />
    <span class="form__input-title required">Цена товара</span>
    <Input class="form__input" placeholder="Введите цену" />
    <Button class="form__btn">Добавить товар</Button>
  </form>
</template>

<script>
import Input from "@/components/Input.vue";
import Button from "@/components/Button.vue";
export default {
  components: {
    Input,
    Button,
  },
};
</script>

<style lang="scss" scoped>
.form {
  padding: $formPadding;
  background-color: $white;
  max-height: $formHeigth;
  width: $formWidth;
  box-shadow: $formBoxShadow;
  border-radius: $formBorderRadius;

  &__input-title {
    display: block;
    font-size: $inputTitleFontSize;
    margin-bottom: 5px;
    font-weight: 300;

    &.required::after {
      content: "";
      display: inline-block;
      width: 4px;
      height: 4px;
      border-radius: 2px;
      background-color: $pink;

      position: relative;
      top: -5px;
      left: 2px;
    }
  }

  &__input + &__input-title {
    margin-top: 16px;
  }

  &__btn {
    margin-top: 24px;
  }
}
</style>
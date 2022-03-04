<template>
  <form class="form" @submit.prevent="addCard">
    <span class="form__input-title required">Наименование товара</span>
    <Input
      class="form__input"
      v-model="name"
      placeholder="Введите наименование товара"
    />
    <span class="form__input-title">Описание товара</span>
    <Input
      class="form__input"
      v-model="description"
      placeholder="Введите описание товара"
      rows="6"
      textarea
    />
    <span class="form__input-title required">Ссылка на изображение товара</span>
    <Input class="form__input" v-model="link" placeholder="Введите ссылку" />
    <span class="form__input-title required">Цена товара</span>
    <Input class="form__input" v-model="price" placeholder="Введите цену" />
    <Button
      :class="['form__btn', checkInputs ? 'enabled' : 'disabled']"
      type="submit"
      >Добавить товар</Button
    >
  </form>
</template>

<script>
import Input from "@/components/Input.vue";
import Button from "@/components/Button.vue";
export default {
  data() {
    return {
      name: "",
      description: "",
      link: "",
      price: "",
      cardsCopy: [],
    };
  },
  props: {
    value: Array,
  },
  components: {
    Input,
    Button,
  },
  methods: {
    addCard() {
      const card = {
        name: this.name,
        description: this.description,
        price: this.price.replace(/\B(?=(\d{3})+(?!\d))/g, " "),
        photo: this.link,
      };
      this.cardsCopy.push(card);
      this.$emit("input", this.cardsCopy);
    },
  },
  computed: {
    checkInputs() {
      return this.name && this.link && this.price;
    },
  },
  created() {
    this.cardsCopy = this.value;
  },
};
</script>

<style lang="scss" scoped>
.form {
  padding: $formPadding;
  background-color: $white;
  max-height: $formHeigth;
  min-width: $formWidth;
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

@media (max-width: 360px) {
  .form {
    min-width: 310px;
  }
}
</style>
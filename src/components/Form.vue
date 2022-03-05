<template>
  <form class="form" @submit.prevent="addCard">
    <label class="form__input-title required">Наименование товара</label>
    <Input
      class="form__input"
      v-model="name"
      placeholder="Введите наименование товара"
    />
    <label class="form__input-title">Описание товара</label>
    <Input
      class="form__input"
      v-model="description"
      placeholder="Введите описание товара"
      rows="6"
      textarea
    />
    <label class="form__input-title required"
      >Ссылка на изображение товара</label
    >
    <Input class="form__input" v-model="link" placeholder="Введите ссылку" />
    <label class="form__input-title required">Цена товара</label>
    <Input
      class="form__input"
      v-model="price"
      @input="maskForPrice"
      placeholder="Введите цену"
    />
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
      if (this.validateInputs()) {
        const card = {
          name: this.name,
          id: Math.random().toString(36).slice(2),
          description: this.description,
          price: this.price.replace(/\B(?=(\d{3})+(?!\d))/g, " "),
          path: this.link,
        };
        this.cardsCopy.unshift(card);
        this.$emit("input", this.cardsCopy);

        this.clearForm();
      } else return;
    },
    clearForm() {
      this.name = "";
      this.description = "";
      this.link = "";
      this.price = "";
    },
    maskForPrice() {
      this.price = this.price
        .replaceAll(" ", "")
        .replace(/\B(?=(\d{3})+(?!\d))/g, " ");
    },
    validateInputs() {
      const regExp = /^\d+$/;
      return (
        this.name !== "" &&
        this.link !== "" &&
        regExp.test(this.price.replaceAll(" ", ""))
      );
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

  &__error {
    color: $black;
    font-size: $inputTitleFontSize;
  }

  &__input-title {
    display: block;
    font-size: $inputTitleFontSize;
    margin-bottom: 5px;

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
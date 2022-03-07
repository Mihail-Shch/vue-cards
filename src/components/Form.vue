<template>
  <form class="form" @submit.prevent="addUser">
    <div class="form__input-wrapper" :class="{ hasError: $v.form.name.$error }">
      <label class="form__input-title required">Наименование товара</label>
      <Input
        class="form__input"
        v-model="form.name"
        placeholder="Введите наименование товара"
      />
      <small
        class="form__error"
        v-if="$v.form.name.$dirty && !$v.form.name.required"
        >Поле обязательно!</small
      >
      <small
        class="form__error"
        v-if="$v.form.name.$dirty && !$v.form.name.minLength"
        >Минимум 4 символа</small
      >
    </div>
    <div class="form__input-wrapper">
      <label class="form__input-title">Описание товара</label>
      <Input
        class="form__input"
        v-model="form.description"
        placeholder="Введите описание товара"
        rows="6"
        textarea
      />
    </div>
    <div class="form__input-wrapper" :class="{ hasError: $v.form.link.$error }">
      <label class="form__input-title required"
        >Ссылка на изображение товара</label
      >
      <Input
        class="form__input"
        v-model="form.link"
        placeholder="Введите ссылку"
      />
      <small
        class="form__error"
        v-if="$v.form.link.$dirty && !$v.form.link.required"
        >Поле обязательно!</small
      >
      <small
        class="form__error"
        v-if="$v.form.link.$dirty && !$v.form.link.minLength"
        >Минимум 4 символа</small
      >
    </div>
    <div
      class="form__input-wrapper"
      :class="{ hasError: $v.form.price.$error }"
    >
      <label class="form__input-title required">Цена товара</label>
      <Input
        class="form__input"
        v-model="form.price"
        placeholder="Введите цену"
      />
      <small
        class="form__error"
        v-if="$v.form.price.$dirty && !$v.form.price.required"
        >Поле обязательно!</small
      >
      <small
        class="form__error"
        v-if="$v.form.price.$dirty && !$v.form.price.between"
        >Введите число между {{ $v.form.price.$params.between.min }} и
        {{ $v.form.price.$params.between.max }}</small
      >
    </div>
    <Button
      :class="['form__btn', $v.form.$anyError ? 'disabled' : 'enabled']"
      type="submit"
      >Добавить товар</Button
    >
  </form>
</template>

<script>
import { minLength, required, between } from "vuelidate/lib/validators";

import Input from "@/components/Input.vue";
import Button from "@/components/Button.vue";
export default {
  data() {
    return {
      form: {
        name: "",
        description: "",
        link: "",
        price: "",
      },
      cardsCopy: [],
    };
  },
  props: {
    value: Array,
  },
  validations: {
    form: {
      name: {
        required,
        minLength: minLength(4),
      },
      price: {
        required,
        between: between(1, 999999),
      },
      link: {
        required,
        minLength: minLength(4),
      },
    },
  },
  components: {
    Input,
    Button,
  },
  methods: {
    addUser() {
      this.$v.form.$touch();
      if (this.$v.form.$pending || this.$v.form.$error) return;

      const card = {
        name: this.form.name,
        id: Math.random().toString(36).slice(2),
        description: this.form.description,
        price: this.form.price.replace(/\B(?=(\d{3})+(?!\d))/g, " "),
        path: this.form.link,
      };
      this.cardsCopy.unshift(card);
      this.$emit("input", this.cardsCopy);

      this.clearForm();
      this.$v.form.$reset();
    },
    clearForm() {
      this.form.name = "";
      this.form.description = "";
      this.form.link = "";
      this.form.price = "";
    },
    // maskForPrice() {
    //   this.form.price = this.form.price
    //     .toString()
    //     .replaceAll(" ", "")
    //     .replace(/\B(?=(\d{3})+(?!\d))/g, " ");
    // },
    // И проверка нормальная на ссылку
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
  height: 100%;
  min-width: $formWidth;
  box-shadow: $formBoxShadow;
  border-radius: $formBorderRadius;

  &__error {
    color: $red;
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

  &__input-wrapper.hasError label {
    color: $red;
  }

  &__input-wrapper.hasError input {
    border-color: $red;
  }

  &__input-wrapper + &__input-wrapper {
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
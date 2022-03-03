<template>
  <div id="app">
    <div class="container">
      <header class="header">
        <h1 class="header__title">Добавление товара</h1>
        <Filters :options="options" />
      </header>
      <div class="content">
        <Form />
        <div class="cards-wrapper">
          <Card v-for="(item, index) in cards" :card="item" :key="index" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Form from "@/components/Form.vue";
import Filters from "@/components/Filters.vue";
import Card from "@/components/Card.vue";
export default {
  name: "App",
  data() {
    return {
      card: {
        name: "Наименование товара",
        description:
          "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
        price: "10 000",
        photo: "@/assets/img/card-photo.png",
      },
      cards: [],
      options: [
        {
          name: "По умолчанию",
          value: 0,
        },
        {
          name: "По цене min",
          value: 1,
        },
        {
          name: "По цене max",
          value: 2,
        },
        {
          name: "По наименованию",
          value: 3,
        },
      ],
    };
  },
  components: {
    Form,
    Filters,
    Card,
  },
  created() {
    this.cards = new Array(12).fill(this.card);
  },
};
</script>

<style lang="scss">
#app {
  padding: 32px 0;
}

.header {
  @extend %between-center;
  margin-bottom: 16px;
}
.header__title {
  font-size: $headerTitleFontSize;
}

.content {
  @extend %between;
}

.cards-wrapper {
  display: grid;
  grid-template-columns: repeat(3, $formWidth);
  grid-template-rows: auto;
  grid-gap: 16px;
}

.card {
  @extend %column;
  &__info {
    background-color: $white;
    padding: $cardInfoPadding;

    &-title {
      font-size: $cardTitleFontSize;
      margin-bottom: 16px;
    }

    &-desc {
      font-size: $cardDescFontSize;
      font-weight: 300;

      margin-bottom: 32px;
    }

    &-price {
      font-size: $cardPriceFontSize;
    }
  }
}
</style>

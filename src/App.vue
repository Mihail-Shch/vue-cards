<template>
  <div id="app">
    <div class="container">
      <header class="header">
        <h1 class="header__title">Добавление товара</h1>
        <Burger @toggle="toggleActive" />
        <Filters v-if="ifOptionsExist" :filters="options" @sort="sortCards" />
      </header>
      <div class="content" v-if="ifCardsExist">
        <Form :class="formClasses" v-model="cards" />
        <div class="cards-wrapper" v-if="cards">
          <Card
            v-for="(item, index) in cards"
            :card="item"
            :key="index"
            @delete="deleteCard"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Form from "@/components/Form.vue";
import Filters from "@/components/Filters.vue";
import Card from "@/components/Card.vue";
import Burger from "@/components/Burger.vue";
export default {
  name: "App",
  data() {
    return {
      options: [],
      cards: [],
      formIsActive: false,
      formClasses: [],
    };
  },
  components: {
    Form,
    Filters,
    Card,
    Burger,
  },
  methods: {
    toggleActive() {
      if (this.formIsActive) {
        this.formClasses = ["fadeOut"];
        setTimeout(() => {
          this.formIsActive = false;
        }, 500);
      } else {
        this.formClasses = ["fadeIn"];
        this.formIsActive = true;
      }
    },
    deleteCard(item) {
      const filteredArr = this.cards.filter((card) => card.id !== item.id);
      this.cards = filteredArr;
    },
    sortCards(option) {
      switch (option.value) {
        case "min":
          this.sortByMinPrice();
          break;
        case "max":
          this.sortByMaxPrice();
          break;
        case "name":
          this.sortByName();
          break;
      }
    },
    deleteSpaces(str) {
      return str.replaceAll(" ", "");
    },
    sortByMinPrice() {
      this.cards = this.cards.sort(
        (a, b) =>
          Number(this.deleteSpaces(a.price)) -
          Number(this.deleteSpaces(b.price))
      );
    },
    sortByMaxPrice() {
      this.cards = this.cards.sort(
        (a, b) =>
          Number(this.deleteSpaces(b.price)) -
          Number(this.deleteSpaces(a.price))
      );
    },
    sortByName() {
      this.cards = this.cards.sort((a, b) => (a.name > b.name ? 1 : -1));
    },
  },
  computed: {
    ifCardsExist() {
      return !!this.cards.length > 0;
    },
    ifOptionsExist() {
      return !!this.options.length > 0;
    },
  },
  async created() {
    const res = await Promise.all([
      fetch("http://localhost:8081/cards"),
      fetch("http://localhost:8081/filters"),
    ]);

    const data = await Promise.all(res.map((r) => r.json()));

    this.cards = data[0];
    this.options = data[1];
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

.form {
  margin-right: 16px;
}

.cards-wrapper {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: auto;
  grid-gap: 16px;
}

@media (max-width: 1420px) {
  .cards-wrapper {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 1070px) {
  .cards-wrapper {
    grid-template-columns: repeat(2, 1fr);
  }

  .header {
    position: relative;
  }

  .form {
    position: absolute;
    z-index: 3;
    opacity: 0;
    transform: translateX(-100%);

    margin-right: 0;

    transition: all 0.5s ease-in-out;
  }

  .form.fadeIn {
    opacity: 1;
    transform: translateX(0);
  }

  .form.fadeOut {
    opacity: 0;
    transform: translateX(-100%);
  }

  .header__title {
    display: none;
  }
}

@media (max-width: 720px) {
  .cards-wrapper {
    grid-template-columns: 1fr;
  }

  .container {
    padding: 0 10px;
  }
}

@media (max-width: 350px) {
  .content {
    justify-content: center;
  }

  .cards-wrapper {
    grid-template-columns: 300px;
  }
}
</style>

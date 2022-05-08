<template>
  <div id="app">
    <div class="container">
      <header class="header">
        <h1 class="header__title">Добавление товара</h1>
        <Burger @toggle="toggleActive" v-model="formIsActive" />
        <Filters :filters="options" v-model="cards" />
      </header>
      <div class="content">
        <Form :class="formClasses" v-model="cards" />
        <div class="cards-wrapper">
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
      options: [
        {
          name: "По умолчанию",
          value: "byDefault",
        },
        {
          name: "По цене min",
          value: "byPriceMinToMax",
        },
        {
          name: "По цене max",
          value: "byPriceMaxToMin",
        },
        {
          name: "По наименованию",
          value: "byTitle",
        },
      ],
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
      const filteredArr = this.cards.filter((card) => card._id !== item._id);
      console.log(filteredArr);
      this.cards = filteredArr;
    },
  },
  async created() {
    const req = await fetch("http://localhost:3000/api/cards");
    const data = await req.json();

    this.cards = data;
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
  font-weight: 600;
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

@media (max-width: 650px) {
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

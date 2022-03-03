<template>
  <div id="app">
    <div class="container">
      <header class="header">
        <h1 class="header__title">Добавление товара</h1>
        <Burger @toggle="toggleActive" />
        <Filters :options="options" />
      </header>
      <div class="content">
        <Form :class="formClasses" />
        <div class="cards-wrapper">
          <Card v-for="(item, index) in 12" :card="card" :key="index" />
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
      card: {
        name: "Наименование товара",
        description:
          "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
        price: "10 000",
      },
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

<template>
  <Header />
  <main class="main">
    <section class="filters">
      <input
        v-model="search"
        placeholder="Pesquisar imóveis"
        class="filter-input"
      />

      <select v-model="priceOrder" name="price_order" class="filter-price">
        <option disabled selected value="default">Ordernar por</option>
        <option value="low_cost">Mais baratos</option>
        <option value="high_cost">Mais caros</option>
      </select>
    </section>

    <CardList :properties="filteredProperties" />
  </main>
</template>

<script>
import Header from "./components/Header.vue";
import CardList from "./components/CardList.vue";

import axios from "axios";

export default {
  name: "App",
  components: {
    Header,
    CardList,
  },
  data() {
    return {
      properties: null,
      priceOrder: "default",
      search: "",
    };
  },
  methods: {
    removeSpecials(text) {
      text = text.replace(/[ÀÁÂÃÄÅ]/, "A");
      text = text.replace(/[àáâãäå]/, "a");
      text = text.replace(/[ÈÉÊË]/, "E");
      text = text.replace(/[èéê]/, "e");
      text = text.replace(/[ÌÍ]/, "I");
      text = text.replace(/[ìí]/, "i");
      text = text.replace(/[Ç]/, "C");
      text = text.replace(/[ç]/, "c");

      return text;
    },
  },
  computed: {
    filteredProperties() {
      let items = [];
      const wordSearch = this.removeSpecials(this.search).toLowerCase();
      items = this.properties.filter((property) => {
        return (
          this.removeSpecials(property.address.toLowerCase()).indexOf(
            wordSearch
          ) > -1 ||
          this.removeSpecials(property.region.toLowerCase()).indexOf(
            wordSearch
          ) > -1
        );
      });
      return items;
    },
  },
  watch: {
    priceOrder: function (order) {
      if (order === "low_cost")
        this.properties.sort((a, b) => a.asking_price - b.asking_price);
      else if (order === "high_cost")
        this.properties.sort((a, b) => b.asking_price - a.asking_price);
    },
  },
  created() {
    axios
      .get("https://development-api.blintz.com.br/properties")
      .then((response) => (this.properties = response.data));
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
}

*,
*::after,
*::before {
  box-sizing: inherit;
}

html {
  --color-0: #f25955;
  --color-1: #666;
  --color-2: #6c757d;
  --color-3: #ef3631;

  --font-0: "Roboto", sans-serif;
  --box-shadow-0: rgba(0, 0, 0, 0.1) 0px 4px 6px -1px,
    rgba(0, 0, 0, 0.06) 0px 2px 4px -1px;
  --box-shadow-1: rgba(0, 0, 0, 0.35) 0px 5px 15px;
  --box-shadow-2: rgba(60, 64, 67, 0.3) 0px 1px 2px 0px,
    rgba(60, 64, 67, 0.15) 0px 2px 6px 2px;

  --header-heigth: 50px;

  box-sizing: border-box;
  font-size: 62.5%; /* 1rem = 10px, 10px/16px = 62.5%*/
  font-family: var(--font-0);
  scroll-behavior: smooth;
}

.main {
  position: relative;
  margin-top: var(--header-heigth);
  padding: 1rem;
}

.filters {
  margin: 1rem 5rem;
  display: flex;
  flex-direction: column;
  gap: 2rem;
}

@media (min-width: 600px) {
  .filters {
    flex-direction: row;
  }
}

.filter-input {
  padding: 1rem;
  font-size: 1.6rem;
  border: none;
  outline: none;
  font-weight: 700;
  border-radius: 0.25rem;
  box-shadow: var(--box-shadow-2);
}

@media (min-width: 600px) {
  .filter-input {
    flex-basis: 400px;
  }
}

.filter-input::placeholder {
  font-weight: 300;
}

.filter-price {
}

@media (min-width: 600px) {
  .filter-price {
    flex-basis: 150px;
  }
}
</style>

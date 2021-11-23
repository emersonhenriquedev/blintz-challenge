<template>
  <div class="card">
    <div class="card-header__img">
      <img
        src="../assets/img/exemplo-de-casa-a-venda-1.jpg"
        alt="Imóvel a venda"
        class="card-header__img"
      />
    </div>
    <div class="card-body">
      <h2>{{ property.address }}</h2>
      <p class="item-region">{{ property.region }}</p>

      <p class="item-type">
        {{ property.property_type }}
        <span v-if="property.building"> - {{ property.building }}</span>
      </p>

      <p class="item-price">{{ currencyInBRL }}</p>

      <a href="#" class="item-cta">Ver imóvel</a>
    </div>
    <div class="card-footer">
      <div class="item-feature">
        <img src="../assets/img/bed.png" alt="Dormitórios" />
        <p>{{ property.bedrooms }}</p>
      </div>

      <div class="item-feature">
        <img src="../assets/img/garage.png" alt="Garagem" />
        <p>{{ property.parking_spots }}</p>
      </div>

      <div class="item-feature">
        <img src="../assets/img/util-area.png" alt="Área" />
        <p>{{ property.area }}m²</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "AppCard",
  props: {
    property: {
      type: Object,
      required: true,
    },
    data() {},
  },

  computed: {
    currencyInBRL() {
      return this.property.asking_price.toLocaleString("pt-br", {
        style: "currency",
        currency: "BRL",
      });
    },
  },
};
</script>

<style scoped>
.card {
  border: 1px solid rgba(0, 0, 0, 0.125);
  border-radius: 0.25rem;
  width: 300px;

  display: flex;
  flex-direction: column;
  justify-content: space-between;

  transition: 0.5s all;
}

.card:hover {
  box-shadow: var(--box-shadow-0);
  box-shadow: var(--box-shadow-1);
}

.card img {
  height: 192px;
  width: 100%;
}

.card-body {
  padding: 1.25rem;
  padding: 2rem;
  font-size: 1.6rem;
  font-weight: 300;
}

.card-body h2 {
  font-size: 2rem;
  font-weight: 400;
  color: var(--color-0);
  margin: 0.5rem 0;
  height: 50px;
}

.item-type {
  color: var(--color-1);
  font-size: 1.5rem;
  margin-top: 0.4rem;
}

.item-price {
  font-weight: 600;
  font-size: 2.3rem;
  color: var(--color-0);
  margin: 2rem 0;
}

.item-cta {
  color: #fff;
  text-decoration: none;
  background-color: var(--color-0);
  border-color: var(--color-0);
  padding: 1rem;
  display: block;
  width: 100%;
  text-align: center;
  font-weight: 400;
  text-shadow: 0px 2px rgba(0, 0, 0, 0.1);
}

.item-cta:hover {
  background-color: #ef3631;
}

.card-footer {
  background-color: rgba(0, 0, 0, 0.03);
  display: flex;
  justify-content: space-around;
  text-align: center;
  padding: 1rem;
}

.card-footer img {
  width: 30px;
  height: 30px;
}

.item-feature {
  font-size: 1.2rem;
  color: var(--color-2);
  font-weight: 600;
}

.item-feature p {
  margin-top: 1rem;
}
</style>
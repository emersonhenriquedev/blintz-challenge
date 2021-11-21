<template>
  <section class="properties">
    <Card
      v-for="(property, index) in properties"
      :key="index"
      :property="property"
      :imgIndex="index"
    >
    </Card>
  </section>
</template>

<script>
import Card from "./Card.vue";
export default {
  name: "AppCardList",
  props: ["properties"],
  data() {
    return {
      imgUrl: "",
    };
  },
  components: {
    Card,
  },
  methods: {},
  computed: {},
};
</script>

<style scoped>
.properties {
  display: flex;
  /* padding: 1rem; */
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 1rem;
}

@media (min-width: 600px) {
  .properties {
    flex-direction: row;
    flex-wrap: wrap;
  }
}
</style>
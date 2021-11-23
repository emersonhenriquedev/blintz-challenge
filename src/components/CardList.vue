<template>
  <section class="properties">
    <Card
      v-for="(property, index) in properties"
      :key="index"
      :property="property"
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
  flex-direction: column;
  align-items: center;
  gap: 1rem;

  height: 517px;
  height: 80vh;
  overflow-y: scroll;
  margin-top: 1.5rem;
}

@media (min-width: 600px) {
  .properties {
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: center;
  }
}
</style>
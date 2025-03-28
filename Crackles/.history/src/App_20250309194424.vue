<template>
  <Nav />
  <main>
    <router-view />
  </main>
</template>

<script>
import Nav from "./components/Nav.vue";
import Ingredients from "./components/Ingredients.vue";

export default {
  name: "App",
  components: {
    Nav,
    Ingredients
  }
};
</script>
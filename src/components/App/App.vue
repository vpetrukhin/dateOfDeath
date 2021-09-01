<template>
  <div class="app">
    <Header />
    <Main />
  </div>
</template>

<script>
import Header from "../Header/Header.vue";
import Main from "../Main/Main.vue";

export default {
  name: "App",
  components: {
    Header,
    Main,
  },
};
</script>

<template>
  <div class="app">
    <Header />
    <Main />
    <Footer />
  </div>
</template>

<script>
import Header from "../Header/Header.vue";
import Main from "../Main/Main.vue";
import Footer from "../Footer/Footer.vue";

export default {
  name: "App",
  components: {
    Header,
    Main,
    Footer,
  },
};
</script>

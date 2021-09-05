<template>
  <div class="app">
    <div v-if="this.quizStates.beginQuiz">
      <Quiz
        :state="this.quizStates"
        v-on:toThirdQuestion="thirdQuestionHandler"
        v-on:toFourthQuestion="fourthQuestionHandler"
        v-on:to-result="resultPageHandler"
      />
    </div>
    <div v-else-if="this.mainIsActive">
      <Header
        v-on:beginQuiz="secondQuestionHandler"
        v-on:scrollToDict="scrollToDict"
      />
      <Main ref="main" v-on:beginQuiz="secondQuestionHandler" />
      <Footer />
    </div>
    <div v-else-if="quizStates.result">
      <result-page />
      <Footer />
    </div>
  </div>
</template>

<script>
import Header from "./Header.vue";
import Main from "./Main.vue";
import Footer from "./Footer.vue";
import Quiz from "./Quiz.vue";
import ResultPage from "./ResultPage.vue";

// Разобраться со скорлом

export default {
  name: "App",
  data: () => ({
    mainIsActive: true,
    quizStates: {
      beginQuiz: false,
      secondQuestion: false,
      thirdQuestion: false,
      result: false,
    },
  }),
  methods: {
    secondQuestionHandler() {
      this.mainIsActive = false;
      this.quizStates.beginQuiz = true;
      this.quizStates.secondQuestion = true;
    },
    thirdQuestionHandler(event) {
      if (event.target.tagName === "BUTTON") {
        this.quizStates.secondQuestion = false;
        this.quizStates.thirdQuestion = true;
      }
    },
    fourthQuestionHandler() {
      this.quizStates.thirdQuestion = false;
    },
    resultPageHandler() {
      this.quizStates.beginQuiz = false;
      this.quizStates.result = true;
      console.log("result");
    },
    scrollToDict() {
      console.log(this.$refs.main);
    },
  },
  components: {
    Header,
    Main,
    Footer,
    Quiz,
    ResultPage,
  },
};
</script>

<style scoped>
.app {
  background: #202024;
}
.app__container {
  max-width: 1440px;
  margin: 0 auto;
}
</style>

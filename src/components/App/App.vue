<template>
  <div class="app">
    <div v-if="this.quizStates.beginQuiz">
      <Quiz
        :state="this.quizStates"
        v-on:toThirdQuestion="thirdQuestionHandler"
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
  </div>
</template>

<script>
import Header from "../Header/Header.vue";
import Main from "../Main/Main.vue";
import Footer from "../Footer/Footer.vue";
import Quiz from "../Quiz/Quiz.vue";

// Разобраться со скорлом
// Разобрать с svg

export default {
  name: "App",
  data: () => ({
    mainIsActive: true,
    quizStates: {
      beginQuiz: false,
      secondQuestion: false,
      thirdQuestion: false,
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
    scrollToDict() {
      console.log(this.$refs.main);
    },
  },
  components: {
    Header,
    Main,
    Footer,
    Quiz,
  },
};
</script>

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
      <div ref="main">
        <Main v-on:beginQuiz="secondQuestionHandler" />
      </div>
      <Footer />
    </div>
    <div v-else-if="quizStates.result">
      <result-page v-on:to-info-page="infoPagehandler" />
      <Footer />
    </div>
    <div v-else-if="infoPageIsActive">
      <info-page :person="person" v-on:to-main-page="mainPageHandler" />
    </div>
  </div>
</template>

<script>
import Header from "./Header.vue";
import Main from "./Main.vue";
import Footer from "./Footer.vue";
import Quiz from "./Quiz.vue";
import ResultPage from "./ResultPage.vue";
import InfoPage from "./infoPage.vue";

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
    infoPageIsActive: false,
    person: {},
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
    },
    infoPagehandler() {
      this.fetchPersonData()
        .then((data) => {
          if (data) {
            this.person = data;
          }
        })
        .catch((err) => {
          console.error(err);
        });
      this.quizStates.result = false;
      this.infoPageIsActive = true;
    },
    mainPageHandler() {
      this.infoPageIsActive = false;
      this.mainIsActive = true;
    },
    async scrollToDict() {
      const top = this.$refs.main.getBoundingClientRect().y - 50;
      const delta = (top - window.scrollY) / 100;
      for (let i = 0; i < 100; i++) {
        // Ожидание 1 секунды, деленного на качетсво анимации
        await new Promise((resolve) => {
          window.setTimeout(function () {
            resolve();
          }, 1000 / 100);
        });
        window.scrollTo(0, window.scrollY + delta);
      }
    },
    fetchPersonData() {
      return fetch("https://swapi.dev/api/people/1/").then((res) =>
        res.ok ? res.json() : Promise.reject(`Ошибка: ${res.status}`)
      );
    },
  },
  components: {
    Header,
    Main,
    Footer,
    Quiz,
    ResultPage,
    InfoPage,
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

<template>
  <section class="quiz">
    <header class="quiz__header" v-if="!this.isLoading">
      <p class="quiz__quote" v-if="state.secondQuestion">
        <img
          src="../../assets/image/eyes.svg"
          alt="eye"
          class="quiz__eye-icon"
        />
        Мы расскажем Вам не только подробности вашей смерти, но также поможем
        Вам избежать этой ужасной даты и продлить вашу жизнь на многие годы.
      </p>
      <p class="quiz__quote" v-else-if="state.thirdQuestion">
        <img
          src="../../assets/image/eyes.svg"
          alt="eye"
          class="quiz__eye-icon"
        />
        Уже совсем скоро Вы узнаете много интересного о своем будущем!
      </p>
      <p class="quiz__quote" v-else-if="this.fourthQuestion">
        <img
          src="../../assets/image/eyes.svg"
          alt="eye"
          class="quiz__eye-icon"
        />
        Смерть родного человека – одно из тяжелейших испытаний в жизни каждого
        из нас!
      </p>
      <div class="quiz__quote-wrapper" v-else-if="this.fifthQuesthion">
        <img
          src="../../assets/image/eyes.svg"
          alt="eye"
          class="quiz__eye-icon"
        />
        <p class="quiz__quote quiz__quote_message">
          {{ this.messageText }}
        </p>
      </div>
    </header>
    <main class="quiz__main">
      <div v-if="state.secondQuestion">
        <h2 class="quiz__title">
          Когда Вы чувствуете себя наиболее комфортно?
        </h2>
        <div
          class="quiz__btns-wrapper"
          @click="$emit('toThirdQuestion', $event)"
        >
          <button class="btn btn_color_yellow quiz__btn" type="button">
            Утро
          </button>
          <button class="btn btn_color_yellow quiz__btn" type="button">
            День
          </button>
          <button class="btn btn_color_yellow quiz__btn" type="button">
            Вечер
          </button>
          <button class="btn btn_color_yellow quiz__btn" type="button">
            Ночь
          </button>
        </div>
        <p class="quethion-num quiz__quethion-num">
          <img
            src="../../assets/image/eye.svg"
            alt="planet"
            class="quiz__planet-icon"
          />
          Вопрос 2-5
        </p>
      </div>
      <div v-else-if="state.thirdQuestion">
        <h2 class="quiz__title">Укажите свою дату рождения:</h2>
        <form
          class="quiz__form"
          @submit.prevent="submitHandler"
          novalidate
          ref="form"
        >
          <input
            type="text"
            class="quiz__input"
            :class="{ quiz__input_error: !isValid }"
            placeholder="День"
            v-model="this.day"
            @input="resetValid"
          />
          <input
            type="text"
            class="quiz__input"
            :class="{ quiz__input_error: !isValid }"
            placeholder="Месяц"
            v-model="this.month"
          />
          <input
            type="text"
            class="quiz__input"
            :class="{ quiz__input_error: !isValid }"
            placeholder="Год"
            v-model="this.year"
          />
          <button class="btn btn_color_yellow quiz__btn" type="submit">
            Далее
          </button>
        </form>
        <p class="quethion-num quiz__quethion-num">
          <img
            src="../../assets/image/eye.svg"
            alt="planet"
            class="quiz__planet-icon"
          />
          Вопрос 3-5
        </p>
      </div>
      <div class="quiz__loader-wrapper" v-else-if="this.isLoading">
        <Loader />
        <p class="quiz__loader-text">Loading</p>
      </div>
      <div v-else-if="this.fourthQuestion">
        <h2 class="quiz__title">Снятся ли Вам умершие люди?</h2>
        <div class="quiz__btns-wrapper" @click="fifthQuesthionHandler">
          <button class="btn btn_color_yellow quiz_btn" type="button">
            Да
          </button>
          <button class="btn btn_color_yellow quiz_btn" type="button">
            Нет
          </button>
          <button class="btn btn_color_yellow quiz_btn" type="button">
            Иногда
          </button>
        </div>
        <p class="quethion-num quiz__quethion-num">
          <img
            src="../../assets/image/eye.svg"
            alt="planet"
            class="quiz__planet-icon"
          />
          Вопрос 4-5
        </p>
      </div>
      <div v-else-if="this.fifthQuesthion">
        <h2 class="quiz__title">
          Запись, которую Вы услышите, может шокировать людей с неокрепшей
          психикой. Вы готовы узнать, что ждет именно Вас?
        </h2>
        <div class="quiz__btns-wrapper" @click="goToRecording">
          <button class="btn btn_color_yellow btn_quiz" type="button">
            Да
          </button>
          <button class="btn btn_color_yellow btn_quiz" type="button">
            Затрудняюсь ответить
          </button>
        </div>
        <p class="quethion-num quiz__quethion-num">
          <img
            src="../../assets/image/eye.svg"
            alt="planet"
            class="quiz__planet-icon"
          />
          Вопрос 5-5
        </p>
      </div>
      <div v-else-if="this.isRecording">record</div>
    </main>
  </section>
</template>

<script>
import Loader from "../Loader/Loader.vue";

export default {
  emits: ["toThirdQuestion", "toFourthQuestion"],
  components: {
    Loader,
  },
  props: {
    state: {
      type: Object,
      required: true,
    },
  },
  data: () => ({
    userAge: 0,
    day: "",
    month: "",
    year: "",
    isValid: true,
    isLoading: false,
    fourthQuestion: false,
    fifthQuesthion: false,
    isRecording: false,
    messageText: "",
  }),
  methods: {
    submitHandler() {
      this.checkValid();
      if (this.isValid) {
        const date = `${this.year}.${this.month}.${this.day}`;
        this.userAge = this.getAge(date);
        this.resetInput();
        this.$emit("toFourthQuestion");
        this.isLoading = true;
        this.loadingHandler();
        this.fourthQuestionHandler();
      }
    },
    fourthQuestionHandler() {
      this.fourthQuestion = true;
    },
    fifthQuesthionHandler(e) {
      if (e.target.tagName === "BUTTON") {
        this.fourthQuestion = false;
        this.getMessageText();
        this.fifthQuesthion = true;
      }
    },
    goToRecording(e) {
      if (e.target.tagName === "BUTTON") {
        this.fifthQuesthion = false;
        this.isRecording = true;
      }
    },
    loadingHandler() {
      setTimeout(() => (this.isLoading = false), 2000);
    },
    checkValid() {
      if (
        this.year.length < 4 ||
        this.year === "" ||
        this.day.length > 2 ||
        this.day === "" ||
        this.month.length > 2 ||
        this.montn === ""
      ) {
        this.isValid = false;
      } else {
        this.isValid = true;
      }
    },
    resetValid() {
      this.isValid = true;
    },
    resetInput() {
      this.day = "";
      this.month = "";
      this.year = "";
    },
    getAge(date) {
      console.log(date);
      return Math.floor(
        (new Date().getTime() - new Date(date)) / (24 * 3600 * 365.25 * 1000)
      );
    },
    getMessageText() {
      if (this.userAge > 18 && this.userAge < 35) this.messageText = "По вам скучает очень близкий человек, которого больше нет в мире живых";
      if (this.userAge > 36 && this.userAge < 45) this.messageText = "По вам скучает очень близкий человек, которого больше нет в мире живых. Возможно это дедушка или бабушка.";
      if (this.userAge > 46) this.messageText = "По вам скучает очень близкий человек, которого больше нет в мире живых. Возможно это кто-то из Ваших родителей.";
    },
  },
};
</script>

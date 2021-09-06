<template>
  <section class="quiz">
    <header
      class="quiz__header"
      v-if="!this.isLoading"
      :class="{ quiz__header_visible: this.isRecording }"
    >
      <p class="quiz__quote" v-if="state.secondQuestion">
        <img src="../assets/image/eyes.svg" alt="eye" class="quiz__eye-icon" />
        Мы расскажем Вам не только подробности вашей смерти, но также поможем
        Вам избежать этой ужасной даты и продлить вашу жизнь на многие годы.
      </p>
      <p class="quiz__quote" v-else-if="state.thirdQuestion">
        <img src="../assets/image/eyes.svg" alt="eye" class="quiz__eye-icon" />
        Уже совсем скоро Вы узнаете много интересного о своем будущем!
      </p>
      <p class="quiz__quote" v-else-if="this.fourthQuestion">
        <img src="../assets/image/eyes.svg" alt="eye" class="quiz__eye-icon" />
        Смерть родного человека – одно из тяжелейших испытаний в жизни каждого
        из нас!
      </p>
      <div class="quiz__quote-wrapper" v-else-if="this.fifthQuesthion">
        <img src="../assets/image/eyes.svg" alt="eye" class="quiz__eye-icon" />
        <p class="message quiz__quote">
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
            src="../assets/image/eye.svg"
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
            @input="resetValid"
          />
          <input
            type="text"
            class="quiz__input"
            :class="{ quiz__input_error: !isValid }"
            placeholder="Год"
            v-model="this.year"
            @input="resetValid"
          />
          <button class="btn btn_color_yellow quiz__btn" type="submit">
            Далее
          </button>
        </form>
        <p class="quethion-num quiz__quethion-num">
          <img
            src="../assets/image/eye.svg"
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
          <button class="btn btn_color_yellow quiz__btn" type="button">
            Да
          </button>
          <button class="btn btn_color_yellow quiz__btn" type="button">
            Нет
          </button>
          <button class="btn btn_color_yellow quiz__btn" type="button">
            Иногда
          </button>
        </div>
        <p class="quethion-num quiz__quethion-num">
          <img
            src="../assets/image/eye.svg"
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
          <button class="btn btn_color_yellow quiz__btn" type="button">
            Да
          </button>
          <button class="btn btn_color_yellow quiz__btn" type="button">
            Затрудняюсь ответить
          </button>
        </div>
        <p class="quethion-num quiz__quethion-num">
          <img
            src="../assets/image/eye.svg"
            alt="planet"
            class="quiz__planet-icon"
          />
          Вопрос 5-5
        </p>
      </div>
      <div class="quiz__recordingbar" v-else-if="this.isRecording">
        <RecordingBar @recording-done="resultHandler" />
      </div>
    </main>
  </section>
</template>

<script>
import Loader from "./Loader.vue";
import RecordingBar from "./RecordingBar.vue";

export default {
  emits: ["toThirdQuestion", "toFourthQuestion", "toResult"],
  components: {
    Loader,
    RecordingBar,
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
    recordPercent: 0,
    messageText: "",
  }),
  methods: {
    submitHandler() {
      this.checkValid();
      if (this.isValid) {
        const date = `${this.year}.${this.month}.${this.day}`;
        this.userAge = this.getAge(date);
        if (this.userAge > 18) {
          this.resetInput();
          this.$emit("toFourthQuestion");
          this.isLoading = true;
          this.loadingHandler();
          this.fourthQuestionHandler();
        } else {
          this.isValid = false;
        }
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
    resultHandler() {
      this.isRecording = false;
      this.$emit("toResult");
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
        Number(this.day) >= 31 ||
        this.month.length > 2 ||
        this.montn === "" ||
        Number(this.month) >= 12
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
      return Math.floor(
        (new Date().getTime() - new Date(date)) / (24 * 3600 * 365.25 * 1000)
      );
    },
    getMessageText() {
      if (this.userAge > 18 && this.userAge < 35)
        this.messageText =
          "По вам скучает очень близкий человек, которого больше нет в мире живых";
      if (this.userAge > 36 && this.userAge < 45)
        this.messageText =
          "По вам скучает очень близкий человек, которого больше нет в мире живых. Возможно это дедушка или бабушка.";
      if (this.userAge > 46)
        this.messageText =
          "По вам скучает очень близкий человек, которого больше нет в мире живых. Возможно это кто-то из Ваших родителей.";
    },
  },
};
</script>

<style scoped>
.quiz {
  height: 100vh;
  padding-top: 21px;
  overflow-x: hidden;
}
.quiz__eye-icon {
  position: absolute;
  bottom: -25px;
  right: -72px;
  opacity: 0.6;
}
.quiz__planet-icon {
  position: absolute;
  bottom: -15px;
  left: -10px;
  opacity: 0.6;
}
.quiz__header {
  margin-bottom: 36px;
  border-bottom: 1px solid rgba(255, 255, 255, 0.2);
}
.quiz__header_visible {
  display: none;
}
.quiz__quote {
  max-width: 235px;
  margin: 0 auto 23px;
  position: relative;
  font-family: BadScript;
  font-weight: 400;
  font-size: 14px;
  line-height: 1.43;
  text-align: center;
  color: rgba(255, 255, 255, 0.6);
}
.quiz__quote-wrapper > .quiz__quote {
  color: #202024;
}
.quiz__title {
  max-width: 288px;
  margin: 0 auto 40px;
  font-family: Roboto;
  font-weight: 400;
  font-size: 16px;
  line-height: 1.56;
  text-align: center;
  text-transform: uppercase;
  color: #f6c866;
}
.quiz__btns-wrapper {
  margin: 0 auto 36px;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.quiz__btn {
  margin-bottom: 20px;
}
.quiz__btn:last-of-type {
  margin-bottom: 0;
}
.quiz__quethion-num {
  max-width: 320px;
  margin: 0 auto;
  position: relative;
}
.quiz__form {
  margin-bottom: 36px;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.quiz__input {
  border: none;
  width: 179px;
  margin-bottom: 20px;
  padding: 12px 0;
  font-family: Roboto;
  font-weight: 400;
  font-size: 14px;
  line-height: 16px;
  color: #202024;
  text-align: center;
  background: linear-gradient(
    90deg,
    rgba(228, 228, 228, 0.9) -6.2%,
    rgba(203, 203, 203, 0.9) 100%
  );
  border-radius: 50px;
}
.quiz__input::placeholder {
  font-family: Roboto;
  font-weight: 400;
  font-size: 14px;
  line-height: 16px;
  color: #202024;
}
.quiz__input:focus {
  outline: none;
}
.quiz__input_error {
  border: 1px solid rgba(238, 83, 83, 1);
}
.quiz__loader-wrapper {
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
.quiz__loader-text {
  margin: 0;
  margin-top: 27px;
  font-family: Roboto;
  font-weight: 300;
  font-size: 12px;
  line-height: 14px;
  letter-spacing: 0.1em;
  color: rgba(255, 255, 255, 0.6);
}
.quiz__quote-wrapper {
  position: relative;
}
.quiz__quote_message {
  max-width: 259px;
}
.quiz__quote-wrapper > .quiz__eye-icon {
  bottom: -25px;
  right: -30px;
}
.quiz__recordingbar {
  height: 100%;
}

@media screen and (min-width: 480px) {
  .quiz__quote {
    max-width: 412px;
    margin-bottom: 37px;
    font-size: 25px;
    line-height: 1.4;
  }
  .quiz__btn {
    margin-bottom: 34px;
  }
  .quiz__title {
    max-width: 503px;
    font-size: 25px;
    line-height: 35px;
  }
  .quiz__btns-wrapper {
    margin-bottom: 183px;
  }
  .quiz__eye-icon {
    width: 146px;
    bottom: -40px;
    right: -125px;
  }
  .quiz__planet-icon {
    width: 90px;
    bottom: 40px;
    left: -100px;
  }
  .quiz__input {
    width: 310px;
    padding: 23px 0;
    font-size: 20px;
    line-height: 23px;
  }
  .quiz__input::placeholder {
    font-size: 20px;
    line-height: 23px;
  }
}
</style>

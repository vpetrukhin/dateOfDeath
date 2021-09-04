<template>
  <section class="quiz">
    <header class="quiz__header">
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
    </main>
  </section>
</template>

<script>
export default {
  emits: ["toThirdQuestion", "toFourthQuethion"],
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
  }),
  methods: {
    submitHandler() {
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

      if (this.isValid) {
        const date = `${this.year}.${this.month}.${this.day}`;
        this.userAge = this.getAge(date);
        this.day = "";
        this.month = "";
        this.year = "";
      }
    },
    resetValid() {
      this.isValid = true;
    },
    getAge(date) {
      console.log(date);
      return Math.floor(
        (new Date().getTime() - new Date(date)) / (24 * 3600 * 365.25 * 1000)
      );
    },
  },
};
</script>

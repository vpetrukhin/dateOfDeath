<template>
  <section class="result-page">
    <p class="message result-page__message">
      Спасибо за Ваши ответы!
      <span class="result-page__message-bold">
        Мы подготовили для Вас персональную аудио запись с вашим прогнозом.
      </span>
    </p>
    <p class="result-page__text">
      Вы можете узнать, как повлиять на события, которые ожидают вас в ближайшем
      будущем.
    </p>
    <h2 class="result-page__title">
      <span class="result-page__title-bold">
        Первое значимое событие может произойти уже {{ tomorowDate }}
      </span>
      , Вам надо быть готовым, что бы последствия не оказались необратимыми.
    </h2>
    <p class="result-page__text">
      Нажмите на кнопку ниже прямо сейчас и наберите наш номер телефона.
      Прослушайте важную информацию!
    </p>
    <button class="btn btn_color_green result-page__btn" type="button">
      Позвонить и прослушать
    </button>
  </section>
</template>

<script>
export default {
  name: "ResultPage",
  date: () => ({
    tomorowDate: 0,
  }),
  computed: {
    tomorowDate() {
      return `${new Date().getDate() + 1}.${
        new Date().getMonth() + 2
      }.${new Date().getFullYear()}`;
    },
  },
  methods: {
    // getTomorowDate() {
    //   // const date = ;
    //   this.tomorowDate = ;
    //   console.log(this.tomorowDate);
    // },
  },
};
</script>

<style>
.result-page {
  height: 100vh;
  padding-top: 24px;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.result-page__message {
  max-width: 259px;
  margin: 0;
  margin-bottom: 35px;
  flex-direction: column;
  align-self: center;
}
.result-page__message-bold {
  font-weight: 700;
  text-align: center;
}
.result-page__text {
  max-width: 219px;
  margin: 0;
  margin-bottom: 20px;
  font-family: Roboto;
  font-weight: 300;
  font-size: 14px;
  line-height: 1.14;
  text-align: center;
  color: #ffffff;
}
.result-page__text:last-of-type {
  max-width: 233px;
}
.result-page__title {
  max-width: 230px;
  margin: 0;
  margin-bottom: 19px;
  padding: 64px 50px 38px;
  font-family: Roboto;
  font-weight: 400;
  font-size: 16px;
  line-height: 1.56;
  text-align: center;
  color: #f6c866;
  border: 1px solid #ffffff;
  border-radius: 3px;
}
.result-page__title-bold {
  display: block;
  font-weight: 700;
  text-transform: uppercase;
}
.result-page__btn {
  width: 217px;
  margin-bottom: 52px;
  font-size: 14px;
  line-height: 16px;
}

@media screen and (min-width: 450px) {
  .result-page__message {
    max-width: 480px;
    font-size: 25px;
    line-height: 35px;
  }
  .result-page__text {
    max-width: 422px;
    margin-bottom: 36px;
    font-size: 25px;
    line-height: 35px;
  }
  .result-page__text:last-of-type {
    max-width: 422px;
  }
  .result-page__title {
    max-width: 480px;
    font-size: 25px;
    line-height: 35px;
  }
}
</style>

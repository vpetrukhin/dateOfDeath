<template>
  <header class="header">
    <div class="header__container">
      <h2 class="header__head-text">Лучшие астрологи и экстрасенсы Румынии</h2>
      <p class="header__uptitle">Точность прогноза: 97%</p>
      <div class="header__logo">
        <img
          src="../assets/image/woman1.png"
          alt="icon1"
          class="header__img"
        />
      </div>
      <h1 class="header__title">
        Вас беспокоит вопрос о том,
        <span class="header__title-upper-case">
          когда Вы покинете этот Мир и при каких обстоятельствах?
        </span>
      </h1>
      <button
        class="btn btn_color_yellow header__btn"
        type="button"
        @click="$emit('beginQuiz')"
      >
        Да
      </button>
      <button
        class="btn btn_color_yellow header__btn"
        type="button"
        @click="$emit('scrollToDict')"
      >
        Нет
      </button>
      <p class="header__subtext">Онлайн предсказание</p>
    </div>
  </header>
</template>

<script>
export default {
  emits: ["beginQuiz", "scrollToDict"],
};
</script>

<style scoped>
.header {
  background: transparent url(../assets/image/blik.png) no-repeat center/100% 850px;
}
.header__container {
  max-width: 1440px;
  margin: 0 auto 25px;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.header__head-text {
  width: 100%;
  margin: 36px 0 12px 0;
  padding-bottom: 19px;
  border-bottom: 1px solid rgba(255, 255, 255, 0.2);
  font-family: Roboto;
  font-weight: 300;
  font-size: 16px;
  line-height: 19px;
  text-align: center;
  letter-spacing: 0.1em;
  color: rgba(255, 255, 255, 0.6);
}
.header__uptitle {
  margin: 0;
  margin-bottom: 40px;
  font-family: Roboto;
  font-weight: 300;
  font-size: 25px;
  line-height: 29px;
  text-align: center;
  letter-spacing: 0.1em;
  color: rgba(255, 255, 255, 0.6);
}

.header__logo {
  width: 390px;
  height: 390px;
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
}
.header__logo::before {
  content: "";
  display: block;
  width: 100%;
  height: 100%;
  background: url(../assets/image/icon1.svg) no-repeat center/cover;
  opacity: 0.2;
}
.header__img {
  width: 237px;
  position: absolute;
  z-index: 2;
}
.header__title {
  max-width: 500px;
  margin: 0;
  font-family: Roboto;
  font-weight: 400;
  font-size: 25px;
  line-height: 1.4;
  text-align: center;
  color: #f6c866;
}
.header__title-upper-case {
  display: block;
  margin-bottom: 40px;
  text-transform: uppercase;
}
.header__btn {
  margin-bottom: 34px;
}
.header__subtext {
  margin: 0;
  margin-bottom: 160px;
  font-family: Roboto;
  font-weight: 300;
  font-size: 16px;
  line-height: 19px;
  text-align: center;
  letter-spacing: 0.1em;
  color: rgba(255, 255, 255, 0.6)
}
@media screen and (max-width: 690px) {
  .header {
    background-size: 100% 620px;
    background-position: 0 37px;
  }
}
@media screen and (max-width: 480px) {
  .header {
    background-size: 112% 64%;
    background-position: 0 37px;
  }
  .header__head-text {
    font-size: 12px;
    line-height: 14px;
  }
  .header__uptitle {
    margin-bottom: 24px;
    font-size: 20px;
    line-height: 23px;
  }
  .header__logo {
    width: 225px;
    height: 225px;
  }
  .header__img {
    width: 137px;
  }
  .header__title {
    max-width: 288px;
    font-size: 16px;
    line-height: 1.56;
  }
  .header__title-upper-case {
    margin-bottom: 23px;
  }
  .header__btn {
    margin-bottom: 20px;
  }
  .header__subtext {
    margin-bottom: 100px;
    font-size: 12px;
    line-height: 14px;
  }
}
</style>

<template>
  <main class="main">
    <article class="article main__article">
      <img src="../assets/image/hands.png" alt="" class="article__img" />
      <p class="article__text">
        Позвольте нам раскрыть эту волнующую тайну и
        <span class="text-yellow">
          с точностью определить дату и время вашей смерти,
        </span>
        а также предшествующую этому событию причину
      </p>
    </article>
    <section class="banner main__banner">
      <div class="banner__overlay">
        <p class="banner__text">
          Многие не верят предсказаниям и мы решили доказать каждому,
          <span class="text-yellow">
            что прогноз может изменить жизнь любого человека!
          </span>
        </p>
      </div>
    </section>
    <section class="first-question">
      <h2 class="first-question__title">Боитесь ли вы умереть?</h2>
      <div class="first-question__btns-wrapper">
        <button
          class="first-question__btn btn btn_color_yellow"
          type="button"
          @click="$emit('beginQuiz', true)"
        >
          Да
        </button>
        <button class="first-question__btn btn btn_color_yellow" type="button">
          Нет
        </button>
      </div>
      <p class="quethion-num first-question__text">Вопрос 1-5</p>
    </section>
    <section class="quote">
      <img src="../assets/image/eyes.svg" alt="eye" class="quote__eye-icon" />
      <img src="../assets/image/eye.svg" alt="planet" class="quote__planet" />
      <img src="../assets/image/rune1.svg" alt="rune" class="quote__rune1" />
      <p class="quote__text">
        Вы, конечно, умрете. И все, с кем вы знакомы, тоже однажды умрут.
      </p>
      <img src="../assets/image/rune2.svg" alt="rune" class="quote__rune2" />
    </section>
  </main>
</template>

<script>
export default {
  emits: ["beginQuiz"],
};
</script>

<style scoped>
/* .main {} */
.main__article {
  margin: 0 auto 69px;
}

.article {
  max-width: 442px;
  position: relative;
  padding: 130px 0 83px 0;
  border: 1px solid #ffffff;
  box-sizing: border-box;
  border-radius: 3px;
}
.article__img {
  display: block;
  width: 135px;
  position: absolute;
  top: calc((135px / 2) * -1);
  left: calc(50% - (135px / 2));
}
.article__text {
  max-width: 331px;
  margin: 0 auto;
  font-family: Roboto;
  font-style: normal;
  font-weight: normal;
  font-size: 25px;
  line-height: 1.4;
  text-align: center;
  color: #ffffff;
}

.banner {
  max-width: 1440px;
  margin: 0 auto;
  height: 606px;
  background: url(../assets/image/image7.jpg) no-repeat center/cover;
}
.banner__overlay {
  height: 100%;
  display: flex;
  background-color: rgba(0, 0, 0, 0.4);
}
.banner__text {
  max-width: 343px;
  margin: auto;
  font-family: Roboto;
  font-size: 25px;
  line-height: 1.4;
  text-align: center;
  color: #ffffff;
}
.main__banner {
  margin-bottom: 133px;
}

/* .first-question {} */
.first-question__title {
  margin: 0;
  margin-bottom: 46px;
  font-family: Roboto;
  font-size: 25px;
  line-height: 29px;
  text-align: center;
  text-transform: uppercase;
  color: #f6c866;
}
.first-question__btns-wrapper {
  max-width: 310px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
}
.first-question__btn {
  margin-bottom: 34px;
}
.first-question__text {
  margin: 0;
}

.quote {
  max-width: 1440px;
  margin: 0 auto;
  padding-top: 105px;
  padding-bottom: 152px;
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
  overflow-x: hidden;
}
.quote__eye-icon {
  display: block;
  width: 296px;
  position: absolute;
  top: -105px;
  right: -131px;
}
.quote__planet {
  display: block;
  width: 164px;
  position: absolute;
  bottom: 48px;
  left: -43px;
}
.quote__rune1 {
  display: block;
  margin-bottom: 80px;
}
.quote__text {
  margin: 0;
  margin-bottom: 80px;
  max-width: 230px;
  font-family: BadScript;
  font-size: 25px;
  line-height: 1.4;
  text-align: center;
  color: #ffffff;
}
.quote__rune2 {
  display: block;
}

@media screen and (max-width: 1000px) {
  .quote {
    padding-top: 61px;
    padding-bottom: 70px;
  }
  .quote__eye-icon {
    width: 83.64px;
    top: 30px;
    right: -29px;
  }
  .quote__planet {
    width: 52px;
    left: -16px;
  }
}

@media screen and (max-width: 450px) {
  .article {
    max-width: 255px;
    padding: 58px 0 32px 0;
  }
  .article__img {
    width: 78px;
    top: calc((78px / 2) * -1);
    left: calc(50% - (78px / 2));
  }
  .article__text {
    max-width: 210px;
    font-size: 16px;
    line-height: 1.56;
  }
  .main__article {
    margin-bottom: 40px;
  }
  .banner {
    height: 301px;
  }
  .main__banner {
    margin-bottom: 53px;
  }
  .banner__text {
    max-width: 219px;
    font-size: 16px;
    line-height: 1.56;
  }
  .first-question__title {
    margin-bottom: 27px;
    font-size: 16px;
    line-height: 19px;
  }
  .first-question__btns-wrapper {
    max-width: 182px;
  }
  .first-question__btn {
    margin-bottom: 20px;
  }
}
</style>

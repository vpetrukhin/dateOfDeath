<template>
  <main class="main">
    <article class="article main__article">
      <img src="../../assets/image/hands.png" alt="" class="article__img" />
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
      <img
        src="../../assets/image/eyes.svg"
        alt="eye"
        class="quote__eye-icon"
      />
      <img
        src="../../assets/image/eye.svg"
        alt="planet"
        class="quote__planet"
      />
      <img src="../../assets/image/rune1.svg" alt="rune" class="quote__rune1" />
      <p class="quote__text">
        Вы, конечно, умрете. И все, с кем вы знакомы, тоже однажды умрут.
      </p>
      <img src="../../assets/image/rune2.svg" alt="rune" class="quote__rune2" />
    </section>
  </main>
</template>

<script>
export default {
  emits: ["beginQuiz"],
};
</script>

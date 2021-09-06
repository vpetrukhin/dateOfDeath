<template>
  <section class="info">
    <h2 class="info__title">Информация о персонаже</h2>
    <div class="info__list">
      <p class="info__text">Имя: {{ person.name }}</p>
      <p class="info__text">Рост: {{ person.height }}</p>
      <p class="info__text">Вес: {{ person.mass }}</p>
      <p class="info__text">Цвет волос: {{ person.hair_color }}</p>
      <p class="info__text">Цвет кожи: {{ person.skin_color }}</p>
      <p class="info__text">Цвет глаз: {{ person.eye_color }}</p>
      <p class="info__text">Год рождения: {{ person.birth_year }}</p>
      <p class="info__text">Пол: {{ person.gender }}</p>
    </div>
    <button
      class="btn btn_color_yellow info__btn"
      type="button"
      @click="this.$emit('toMainPage')"
    >
      На главную
    </button>
  </section>
</template>

<script>
export default {
  name: "infoPage",
  emits: ["toMainPage"],
  props: {
    person: {
      type: Object,
    },
  },
};
</script>

<style scoped>
.info {
  height: 100vh;
  padding-top: 20px;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.info__title {
  margin: 0;
  margin-bottom: 20px;
  font-family: Roboto;
  font-weight: 400;
  font-size: 16px;
  line-height: 1.56;
  text-align: center;
  color: #f6c866;
}
.info__list {
  margin: 0;
  padding: 0;
  list-style: none;
  width: 90%;
  margin-bottom: 20px;
}
.info__text {
  margin: 0;
  font-family: Roboto;
  font-weight: 300;
  font-size: 14px;
  line-height: 1.14;
  color: #ffffff;
}
.info__text:not(:last-of-type) {
  margin-bottom: 10px;
}
.info__btn {
  margin-bottom: 10px;
}
</style>

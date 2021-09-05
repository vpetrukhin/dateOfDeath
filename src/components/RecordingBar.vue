<template>
  <div class="recording-bar">
    <img
      src="../assets/image/microphone.svg"
      alt="microphone"
      class="recording-bar__microphone"
    />
    <div class="recording-bar__progress-bar">
      <div
        class="recording-bar__percentage"
        :style="{ width: percentage + '%' }"
      />
    </div>
    <p class="recording-bar__percent">{{ percent }}%</p>
    <p class="recording-bar__text">Запись сообщения</p>
  </div>
</template>

<script>
export default {
  emits: ["recordingDone"],
  data: () => ({
    percentage: 0,
    recording: false,
  }),
  computed: {
    percent() {
      return this.percentage.toFixed();
    },
  },
  created() {
    const intval = setInterval(() => {
      if (this.percentage < 100) {
        this.percentage += 0.1;
      } else {
        this.goToResult();
        clearInterval(intval);
      }
    }, 1);
  },
  methods: {
    goToResult() {
      this.$emit("recordingDone");
    },
  },
};
</script>

<style scoped>
.recording-bar {
  min-height: 500px;
  height: 100%;
  padding: 0 30px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
.recording-bar__microphone {
  display: block;
  margin-bottom: 40px;
}
.recording-bar__progress-bar {
  position: relative;
  width: 100%;
  height: 4px;
  background: #ffffff;
  border-radius: 5px;
  overflow: hidden;
}
.recording-bar__percentage {
  display: block;
  height: 100%;
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  background: #f6c866;
  border-radius: 5px;
}
.recording-bar__percent {
  font-family: Roboto;
  font-weight: 300;
  font-size: 20px;
  line-height: 23px;
  letter-spacing: 0.1em;
  color: rgba(255, 255, 255, 0.6);
}
.recording-bar__text {
  font-family: Roboto;
  font-weight: 300;
  font-size: 12px;
  line-height: 14px;
  letter-spacing: 0.1em;
  text-align: center;
  color: rgba(255, 255, 255, 0.6);
}
</style>

<template>
  <div class="advice-modal-wrapper">
    <div class="advice-modal-body">
      <div class="advice-header">Advice # {{ advice.id }}</div>
      <div class="advice-advice">"{{ advice.advice }}"</div>
      <div class="advice-hr" />
      <div class="advice-roll-button">
        <BtnDice @click="rollAdvice" />
      </div>
    </div>
  </div>
</template>

<script>
import BtnDice from "./general/BtnDice.vue";
export default {
  components: {
    BtnDice,
  },
  props: {
    advice: { type: Object, default: () => ({ id: 0, advice: "" }) },
  },
  emits: ["rollAdvice"],
  methods: {
    rollAdvice() {
      this.$emit("rollAdvice");
    },
  },
};
</script>

<style lang="scss">
@import "@/scss/_vars.scss";
.advice-modal-wrapper {
  display: flex;
  position: relative;
  z-index: 1;
  max-width: 30em;
  justify-content: center;
  align-items: center;
  margin: 0 auto 4.5em;
  padding: 0 0.5em;

  @media (min-width: $device-lg) {
    max-width: 20em;
    min-width: 20em;
    margin-bottom: 0;
  }

  .advice-modal-body {
    display: grid;
    grid-template-columns: 1fr;
    grid-template-rows: 1em 1fr 1em 2em;
    grid-gap: 1em;
    background: $color-dark-grayish-blue;
    border-radius: 0.7em;
    padding: 1.5em 1em 0 1em;
    margin: auto;
    min-width: 90vw;
    min-height: 10em;
    @media (min-width: $device-lg) {
      min-width: 0;
    }

    .advice-header {
      font-size: 0.5em;
      color: $color-neon-green;
      text-transform: uppercase;
      letter-spacing: 0.19em;
      text-align: center;
    }
    .advice-advice {
      text-align: center;
      line-height: 1.5em;
    }
    .advice-hr {
      position: relative;
      z-index: 2;
      width: 10em;
      height: 1em;
      margin: 0 auto;
      background-position: center;
      background-repeat: no-repeat;
      background-size: cover;
      background-image: url("../assets/images/pattern-divider-mobile.svg");
      @media (min-width: $device-lg) {
        background-image: url("../assets/images/pattern-divider-mobile.svg");
      }
    }

    .advice-roll-button {
      position: relative;
      z-index: 2;
      width: 100%;
      display: flex;
      justify-content: center;
      align-items: center;
      transform: translateY(1em);
    }
  }
}
</style>

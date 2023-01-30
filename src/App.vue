<template>
  <div class="wrapper">
    <AdviceModal
      :opened="modalOpened"
      :advice="advice"
      @roll-advice="rerollAdvice"
    />
  </div>
</template>

<script>
import AdviceModal from "@/components/AdviceModal.vue";

export default {
  components: {
    AdviceModal,
  },
  data: () => {
    return {
      modalOpened: false,
      advice: {
        id: 0,
        advice: "Loading...",
      },
    };
  },
  async created() {
    await this.loadAdvice();
  },
  methods: {
    async loadAdvice() {
      try {
        const resp = await fetch("https://api.adviceslip.com/advice");
        if (resp.ok) {
          const data = await resp.json();
          console.log(data);
          if (data?.slip) {
            this.advice = data.slip;
          }
        }
      } catch (e) {
        console.error(e);
      }
    },
    openModal: () => {},
    rerollAdvice: () => {
      this.loadAdvice();
    },
  },
};
</script>

<style lang="scss">
@import "@/scss/index.scss";

html {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

body,
* {
  font-family: "Montagu Slab", serif;
  font-weight: 500;
  font-size: 22px;
  font-variant: normal;
  line-height: 1.2em;
  color: $color-light-cyan;
  box-sizing: border-box;
  @media (min-width: $device-lg) {
    font-size: 28px;
  }
}

body {
  background: $color-dark-blue;
  min-width: 100vw;
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: flex-start;
  padding: 0;
  margin: 0;
}

#app {
  width: 100%;
  height: 100%;
}
</style>

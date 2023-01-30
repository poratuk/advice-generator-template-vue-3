<template>
  <div class="wrapper">
    <transition mode="out-in" name="fade" @leave="checkLoaded">
      <div v-if="modalOpened" class="advice-transition-wrapper">
        <AdviceModal
          key="advice"
          :opened="modalOpened"
          :advice="advice"
          @roll-advice="loadAdvice"
        />
      </div>
    </transition>
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
      transitionActive: false,
      advice: {
        id: 0,
        advice: "Loading...",
      },
    };
  },
  computed: {
    modalOpened() {
      return this.advice.id && !this.transitionActive;
    },
  },
  async created() {
    await this.loadAdvice();
  },
  methods: {
    async loadAdvice() {
      this.advice.id = 0;
      try {
        const resp = await fetch("https://api.adviceslip.com/advice");

        if (resp.ok) {
          const data = await resp.json();
          if (data?.slip) {
            this.advice = data.slip;
          }
        }
      } catch (e) {
        console.error(e);
      }
    },
    checkLoaded() {
      this.transitionActive = false;
    },
  },
};
</script>

<style lang="scss">
@import "@/scss/index.scss";
@import "@/scss/_animation.scss";

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

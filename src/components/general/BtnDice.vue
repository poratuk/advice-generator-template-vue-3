<template>
  <button class="roll-button">
    <img src="@/assets/images/icon-dice.svg" />
  </button>
</template>

<script>
export default {};
</script>

<style lang="scss" scope>
@import "@/scss/_vars.scss";
.roll-button {
  display: block;
  position: relative;
  z-index: 1;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 0.8em;
  background: $color-neon-green;
  color: $color-light-cyan;
  border: none;
  border-radius: 50%;
}
</style>

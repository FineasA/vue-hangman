<template>
  <div class="container">
    <div class="lose-container">
      <h2 class="lose-message">You Lose!</h2>
      <b-button variant="info" @click="resetGame">Try Again?</b-button>
    </div>
  </div>
</template>

<script>
import { EventBus } from "../main.js";

export default {
  methods: {
    resetGame() {
      EventBus.$emit("reset-game");
    }
  }
};
</script>

<style>
.lose-container {
  padding: 2.2rem;
}
.lose-message {
  font-size: 84px;
  color: rgba(255, 0, 0, 0.5);
}
</style>
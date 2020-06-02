<template>
  <div class="container">
    <div class="winner-container">
      <h2 class="winner-message">You win!</h2>
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
.winner-container {
  padding: 2.2rem;
}
.winner-message {
  font-size: 84px;
  color: rgba(255, 0, 0, 0.5);
}
</style>
<template>
  <div class="container page-container">
    <div class="custom-container">
      <h3 class="custom-title">Hangman</h3>
    </div>
    <hangman-display></hangman-display>
    <word-display></word-display>
    <letter-display v-if="!gameEnded"></letter-display>
    <transition name="component-fade" mode="out-in">
      <!-- win/lose components here -->
      <lose :is="currentComponent"></lose>
    </transition>
  </div>
</template>

<script>
import { EventBus } from "./main.js";

import HangmanDisplay from "./components/HangmanDisplay.vue";
import LetterDisplay from "./components/LetterDisplay.vue";
import WordDisplay from "./components/WordDisplay.vue";
import Lose from "./components/Lose.vue";
import Win from "./components/Win.vue";

export default {
  components: {
    HangmanDisplay,
    LetterDisplay,
    WordDisplay,
    Lose,
    Win
  },
  data() {
    return {
      currentComponent: null,
      gameEnded: false
    };
  },
  created() {
    EventBus.$on("lose", () => {
      this.currentComponent = "lose";
      this.gameEnded = true;
    });

    EventBus.$on("winner", () => {
      this.currentComponent = "win";
      this.gameEnded = true;
    });

    EventBus.$on("reset-game", () => {
      this.currentComponent = null;
      this.gameEnded = false;
    });
  }
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Titillium+Web&display=swap");

.container {
  background-color: #ffdbd5;
  border-radius: 20px;
}
.page-container {
  margin-top: 1.2rem;
  border: 2px solid #e2d5ff;
}
.custom-container {
  padding: 20px;
  margin: 1.2rem;
  width: 100%;
  background-color: #ffdbd5;
  border-radius: 20px;
}
.container {
  text-align: center;
}
.custom-title {
  font-family: "Titillium Web", sans-serif;
  font-size: calc(12vw);
}
h3 {
  display: inline;
  position: relative;
  letter-spacing: -5px;
  color: rgba(0, 0, 255, 0.5);
}

h3:after {
  content: "Hangman";
  position: absolute;
  left: 5px;
  top: 22px;
  color: rgba(255, 0, 0, 0.5);
}
</style>
<template>
  <div class="container">
    <div class="hangman-display">
      <img v-if="hangmanSteps === 6" src="../assets/hangman/4.jpg" alt />
      <img v-if="hangmanSteps === 5" src="../assets/hangman/5.jpg" alt />
      <img v-if="hangmanSteps === 4" src="../assets/hangman/6.jpg" alt />
      <img v-if="hangmanSteps === 3" src="../assets/hangman/7.jpg" alt />
      <img v-if="hangmanSteps === 2" src="../assets/hangman/8.jpg" alt />
      <img v-if="hangmanSteps === 1" src="../assets/hangman/9.jpg" alt />
      <img v-if="hangmanSteps === 0" src="../assets/hangman/10.jpg" alt />
    </div>
  </div>
</template>

<script>
import { EventBus } from "../main.js";

export default {
  data() {
    return {
      hangmanSteps: 6,
      imgSrc: "0.jpg"
    };
  },
  created() {
    EventBus.$on("incorrect-letter", incorrectLetter => {
      console.log(incorrectLetter);
      //might do something with the incorrect letter in this component later
      this.hangmanSteps--;
    });
    EventBus.$on("reset-game", () => {
      this.hangmanSteps = 6;
    });
  },
  updated() {
    if (this.hangmanSteps === 0) {
      EventBus.$emit("lose");
    }
  }
};
</script>

<style>
.hangman-steps {
  font-family: "Titillium Web", sans-serif;
  font-size: 200px;
  color: rgba(255, 0, 0, 0.5);
  margin-top: 2.2rem;
}
.hangman-display {
  margin: 0 auto;
  padding: 0.2rem;
  height: 358px;
  width: 208px;
}

img {
  border-radius: 10px;
  border: 2px solid rgba(0, 0, 255, 0.5) !important;
}
</style>
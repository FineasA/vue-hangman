<template>
  <div class="container">
    <div class="word-container">
      <span class="word-display">{{replacedWordDash.join(' ')}}</span>
    </div>
  </div>
</template>

<script>
import { EventBus } from "../main.js";

export default {
  methods: {
    getDashedWord() {
      for (let i = 0; i < this.words[this.randIndex].length; i++) {
        this.replacedWordDash.push("_");
      }
    },
    getRandWord() {
      this.randIndex = Math.floor(
        Math.random() * Math.floor(this.words.length)
      );
      console.log("word: ", this.words[this.randIndex]);
    },
    checkWordForLetter() {
      let tempSplitWord = this.words[this.randIndex].split("");

      if (this.words[this.randIndex].includes(this.letterSelected)) {
        for (let i = 0; i < tempSplitWord.length; i++) {
          if (tempSplitWord[i] === this.letterSelected) {
            this.indexesMarked.push(i);
          }
        }
        for (let j = 0; j < this.indexesMarked.length; j++) {
          this.replacedWordDash.splice(
            this.indexesMarked[j],
            1,
            this.letterSelected
          );
        }
        console.log("indexes:  ", this.indexesMarked);
        EventBus.$emit("correct-letter", this.letterSelected);
        this.checkWin();
        this.indexesMarked = [];
        this.letterSelected = "";
      } else {
        //make button not clickable
        EventBus.$emit("incorrect-letter", this.letterSelected);
      }
    },
    checkWin() {
      if (!this.replacedWordDash.join("").includes("_")) {
        EventBus.$emit("winner");
      }
    }
  },
  data() {
    return {
      replacedWordDash: [],
      randIndex: 0,
      letterSelected: "",
      indexesMarked: [],
      words: [
        "rhythym",
        "fluff",
        "jazz",
        "bookworm",
        "blizzard",
        "kilobyte",
        "syndrome",
        "quartz",
        "yippee",
        "glyph",
        "joyful",
        "kiwifruit",
        "pneumonia"
      ]
    };
  },
  created() {
    this.getRandWord();
    this.getDashedWord();
    EventBus.$on("selected-letter", letterSelected => {
      console.log(letterSelected);
      this.letterSelected = letterSelected;
      //check if letter matches in word
      this.checkWordForLetter();
    });

    EventBus.$on("reset-game", () => {
      this.replacedWordDash = [];
      this.randIndex = 0;
      this.letterSelected = "";
      this.indexesMarked = [];

      this.getRandWord();
      this.getDashedWord();
    });
  }
};
</script>

<style>
.word-display {
  font-family: "Titillium Web", sans-serif;
  font-size: 32px;
  color: rgba(255, 0, 0, 0.5);
}
</style>
<template>
  <div class="container">
    <div class="letter-container">
      <b-button
        v-model="letterSelected"
        @click="selectLetter(letter.letter)"
        variant="info"
        :style="letter.isNotInWord ? 'background-color: #ff938b !important' 
        : (letter.selected && !letter.isNotInWord) ? 'background-color: #8bffac!important' : null"
        class="custom-buttons"
        v-for="(letter, index) in alphabet"
        :key="index"
      >{{letter.letter}}</b-button>
    </div>
  </div>
</template>

<script>
import { EventBus } from "../main.js";

export default {
  methods: {
    selectLetter(letter) {
      this.letterSelected = letter;
      EventBus.$emit("selected-letter", this.letterSelected);
    }
  },
  data() {
    return {
      alphabet: [
        {
          letter: "a",
          selected: false,
          isNotInWord: false
        },
        {
          letter: "b",
          selected: false,
          isNotInWord: false
        },
        {
          letter: "c",
          selected: false,
          isNotInWord: false
        },
        {
          letter: "d",
          selected: false,
          isNotInWord: false
        },
        {
          letter: "e",
          selected: false,
          isNotInWord: false
        },
        {
          letter: "f",
          selected: false,
          isNotInWord: false
        },
        {
          letter: "g",
          selected: false,
          isNotInWord: false
        },
        {
          letter: "h",
          selected: false,
          isNotInWord: false
        },
        {
          letter: "i",
          selected: false,
          isNotInWord: false
        },
        {
          letter: "j",
          selected: false,
          isNotInWord: false
        },
        {
          letter: "k",
          selected: false,
          isNotInWord: false
        },
        {
          letter: "l",
          selected: false,
          isNotInWord: false
        },
        {
          letter: "m",
          selected: false,
          isNotInWord: false
        },
        {
          letter: "n",
          selected: false,
          isNotInWord: false
        },
        {
          letter: "o",
          selected: false,
          isNotInWord: false
        },
        {
          letter: "p",
          selected: false,
          isNotInWord: false
        },
        {
          letter: "q",
          selected: false,
          isNotInWord: false
        },
        {
          letter: "r",
          selected: false,
          isNotInWord: false
        },
        {
          letter: "s",
          selected: false,
          isNotInWord: false
        },
        {
          letter: "t",
          selected: false,
          isNotInWord: false
        },
        {
          letter: "u",
          selected: false,
          isNotInWord: false
        },
        {
          letter: "v",
          selected: false,
          isNotInWord: false
        },
        {
          letter: "w",
          selected: false,
          isNotInWord: false
        },
        {
          letter: "x",
          selected: false,
          isNotInWord: false
        },
        {
          letter: "y",
          selected: false,
          isNotInWord: false
        },
        {
          letter: "z",
          selected: false,
          isNotInWord: false
        }
      ],
      letterSelected: "",
      lettersSelected: []
    };
  },
  created() {
    EventBus.$on("incorrect-letter", incorrectLetter => {
      console.log("Incorrect Letter from LetterDisplay.vue: ", incorrectLetter);
      for (let i = 0; i < this.alphabet.length; i++) {
        if (this.alphabet[i].letter === incorrectLetter) {
          this.alphabet[i].isNotInWord = true;
        }
      }
    });
    EventBus.$on("correct-letter", correctLetter => {
      console.log(correctLetter);
      for (let i = 0; i < this.alphabet.length; i++) {
        if (this.alphabet[i].letter === correctLetter) {
          this.alphabet[i].selected = true;
        }
      }
    });

    EventBus.$on("reset-game", () => {
      this.alphabet = [
        {
          letter: "a",
          selected: false,
          isNotInWord: false
        },
        {
          letter: "b",
          selected: false,
          isNotInWord: false
        },
        {
          letter: "c",
          selected: false,
          isNotInWord: false
        },
        {
          letter: "d",
          selected: false,
          isNotInWord: false
        },
        {
          letter: "e",
          selected: false,
          isNotInWord: false
        },
        {
          letter: "f",
          selected: false,
          isNotInWord: false
        },
        {
          letter: "g",
          selected: false,
          isNotInWord: false
        },
        {
          letter: "h",
          selected: false,
          isNotInWord: false
        },
        {
          letter: "i",
          selected: false,
          isNotInWord: false
        },
        {
          letter: "j",
          selected: false,
          isNotInWord: false
        },
        {
          letter: "k",
          selected: false,
          isNotInWord: false
        },
        {
          letter: "l",
          selected: false,
          isNotInWord: false
        },
        {
          letter: "m",
          selected: false,
          isNotInWord: false
        },
        {
          letter: "n",
          selected: false,
          isNotInWord: false
        },
        {
          letter: "o",
          selected: false,
          isNotInWord: false
        },
        {
          letter: "p",
          selected: false,
          isNotInWord: false
        },
        {
          letter: "q",
          selected: false,
          isNotInWord: false
        },
        {
          letter: "r",
          selected: false,
          isNotInWord: false
        },
        {
          letter: "s",
          selected: false,
          isNotInWord: false
        },
        {
          letter: "t",
          selected: false,
          isNotInWord: false
        },
        {
          letter: "u",
          selected: false,
          isNotInWord: false
        },
        {
          letter: "v",
          selected: false,
          isNotInWord: false
        },
        {
          letter: "w",
          selected: false,
          isNotInWord: false
        },
        {
          letter: "x",
          selected: false,
          isNotInWord: false
        },
        {
          letter: "y",
          selected: false,
          isNotInWord: false
        },
        {
          letter: "z",
          selected: false,
          isNotInWord: false
        }
      ];
      this.letterSelected = "";
      this.lettersSelected = [];
    });
  }
};
</script>

<style>
.letter-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
  margin: auto;
  padding: 2.2rem;
  max-width: 1000px;
}
.custom-buttons {
  width: 85px;
  font-family: "Titillium Web", sans-serif;
  font-size: 32px !important;
  background-color: #d5ffef !important;
  padding: 1.2rem !important;
  color: black !important;
  margin: 0.5rem;
}
.custom-buttons:hover {
  background-color: #92e6c6 !important;
}
</style>
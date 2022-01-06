<template>
  <h1>Wardle®</h1>
  <h3 v-if="this.round === 1" style="color: green">Easy</h3>
  <h3 v-if="this.round === 2" style="color: yellow">Medium</h3>
  <h3 v-if="this.round === 3" style="color: red">Hard</h3>
  <button @click="startGame" v-if="this.round === 0">Start Game</button>
  <button @click="nextRound" v-if="this.is_round_over && !this.is_game_over">
    Next Round
  </button>
  <h2 v-if="this.is_game_over">{{ this.game_over_msg }}</h2>
  <Stopwatch ref="stopwatchRef" />
  <LetterGrid
    v-bind:letterArray="this.letterArray"
    v-bind:rightSpot="this.rightSpot"
    v-bind:rightLetter="this.rightLetter"
  />
  <Keyboard
    @fill-tile="fillTile"
    @backspace="backspace"
    @check-word="checkWord"
    v-if="showKeyboard"
    ref="keyboardRef"
  />
</template>

<script>
import Stopwatch from "./components/Stopwatch";
import LetterGrid from "./components/LetterGrid";
import Keyboard from "./components/Keyboard";

export default {
  name: "App",
  components: {
    Stopwatch,
    LetterGrid,
    Keyboard,
  },
  data: () => ({
    letterArray: [[], [], [], [], [], []],
    words: ["spike", "clear", "ghost"],
    word: "spike",
    rightSpot: [],
    rightLetter: [],
    game_over_msg: "",
    is_game_over: false,
    difficulty: "Easy",
    round: 0,
    is_round_over: false,
    showKeyboard: false,
    triesCount: 0,
  }),
  methods: {
    startGame() {
      this.round++;
      this.$refs.stopwatchRef.start();
      this.showKeyboard = true;
    },
    fillTile(button, row) {
      if (!this.is_game_over && !this.is_round_over) {
        this.letterArray[row].push(button);
      }
    },
    backspace(row) {
      if (!this.is_game_over) {
        this.letterArray[row] = this.letterArray[row].slice(0, -1);
      }
    },
    checkWord(word, row) {
      if (word === this.word) {
        this.is_round_over = true;
        for (let i = 0; i < this.word.length; i++) {
          // right spot
          this.rightSpot.push(row + "" + i);
        }

        this.triesCount += row + 1;

        if (this.round === 3) {
          this.is_game_over = true;
          this.game_over_msg =
            "Congratulations! You completed all 3 rounds in " +
            this.triesCount +
            " total tries!";
          this.$refs.stopwatchRef.stop();
          this.showKeyboard = false;
        }
      } else {
        for (let i = 0; i < this.word.length; i++) {
          if (this.word[i] === word[i]) {
            // right spot
            this.rightSpot.push(row + "" + i);
          } else {
            for (let j = 0; j < this.word.length; j++) {
              if (this.word[j] === word[i]) {
                // right letter
                this.rightLetter.push(row + "" + i);
              }
            }
          }
        }
      }
      if (row === 5 && word !== this.word) {
        this.game_over_msg =
          "Tough Scene. You didn't get the word: " + this.word.toUpperCase();
        this.is_game_over = true;
        this.$refs.stopwatchRef.stop();
      }
    },
    nextRound() {
      this.is_round_over = false;
      this.round++;
      this.word = this.words[this.round - 1];
      this.letterArray = [[], [], [], [], [], []];
      this.$refs.keyboardRef.reset();
      this.rightSpot = [];
      this.rightLetter = [];
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  width: 400px;
  margin: 0 auto;
}
h1 {
  color: white;
}
h2 {
  color: rgb(97, 112, 174);
}
button {
  padding: 10px;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  border: none;
  border-radius: 5px;
}
button:hover {
  background-color: rgb(12, 164, 30);
  color: white;
  cursor: pointer;
}
</style>

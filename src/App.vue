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
  <div class="invalid-word">{{ this.invalidMsg }}</div>
  <LetterGrid
    v-bind:letterArray="this.letterArray"
    v-bind:rightSpot="this.rightSpot"
    v-bind:rightLetter="this.rightLetter"
  />
  <Keyboard
    @fill-tile="fillTile"
    @backspace="backspace"
    @check-word="checkWord"
    @invalid-word="invalidWord"
    v-if="showKeyboard"
    v-bind:greenKey="this.greenKey"
    v-bind:yellowKey="this.yellowKey"
    v-bind:grayKey="this.grayKey"
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
  data() {
    // eslint-disable-next-line prettier/prettier
    // let word_list = ["abuse", "adult", "agent", "anger", "apple", "award", "basis", "beach", "birth", "block", "blood", "board", "brain", "bread", "break", "brown", "buyer", "cause", "chain", "chair", "chest", "chief", "child", "china", "claim", "class", "clock", "coach", "coast", "court", "cover", "cream", "crime", "cross", "crowd", "crown", "cycle", "dance", "death", "depth", "doubt", "draft", "drama", "dream", "dress", "drink", "drive", "earth", "enemy", "entry", "error", "event", "faith", "fault", "field", "fight", "final", "floor", "focus", "force", "frame", "frank", "front", "fruit", "glass", "grant", "grass", "green", "group", "guide", "heart", "henry", "horse", "hotel", "house", "image", "index", "input", "issue", "japan", "jones", "judge", "knife", "laura", "layer", "level", "lewis", "light", "limit", "lunch", "major", "march", "match", "metal", "model", "money", "month", "motor", "mouth", "music", "night", "noise", "north", "novel", "nurse", "offer", "order", "other", "owner", "panel", "paper", "party", "peace", "peter", "phase", "phone", "piece", "pilot", "pitch", "place", "plane", "plant", "plate", "point", "pound", "power", "press", "price", "pride", "prize", "proof", "queen", "radio", "range", "ratio", "reply", "right", "river", "round", "route", "rugby", "scale", "scene", "scope", "score", "sense", "shape", "share", "sheep", "sheet", "shift", "shirt", "shock", "sight", "simon", "skill", "sleep", "smile", "smith", "smoke", "sound", "south", "space", "speed", "spite", "sport", "squad", "staff", "stage", "start", "state", "steam", "steel", "stock", "stone", "store", "study", "stuff", "style", "sugar", "table", "taste", "terry", "theme", "thing", "title", "total", "touch", "tower", "track", "trade", "train", "trend", "trial", "trust", "truth", "uncle", "union", "unity", "value", "video", "visit", "voice", "waste", "watch", "water", "while", "white", "whole", "woman", "world", "youth"];
    // let three_words = word_list.sort(() => 0.5 - Math.random()).slice(0, 3);
    // let first_word = three_words[0];

    return {
      letterArray: [[], [], [], [], [], []],
      words: ["speck", "facts", "vague"],
      word: "speck",
      rightSpot: [],
      rightLetter: [],
      greenKey: [],
      yellowKey: [],
      grayKey: [],
      game_over_msg: "",
      is_game_over: false,
      difficulty: "Easy",
      round: 0,
      is_round_over: false,
      showKeyboard: false,
      triesCount: 0,
      invalidMsg: "",
    };
  },
  mounted() {},
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
      this.invalidMsg = "";
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
            this.greenKey.push(word[i].toUpperCase());
            if (this.yellowKey.includes(word[i].toUpperCase())) {
              this.yellowKey = this.yellowKey.filter(function (f) {
                return f !== word[i].toUpperCase();
              });
            }
          } else {
            for (let j = 0; j < this.word.length; j++) {
              if (this.word[j] === word[i]) {
                // right letter
                this.rightLetter.push(row + "" + i);
                if (!this.greenKey.includes(word[i].toUpperCase())) {
                  this.yellowKey.push(word[i].toUpperCase());
                }
              }
            }
            if (
              !this.greenKey.includes(word[i].toUpperCase()) &&
              !this.yellowKey.includes(word[i].toUpperCase())
            ) {
              this.grayKey.push(word[i].toUpperCase());
            }
          }
        }
      }
      if (row === 5 && word !== this.word) {
        this.game_over_msg =
          "Tough Scene. You didn't get the word: " + this.word.toUpperCase();
        this.is_game_over = true;
        this.$refs.stopwatchRef.stop();
        this.showKeyboard = false;
      }
    },
    invalidWord(word) {
      this.invalidMsg = word.toUpperCase() + " is not a valid word.";
      setTimeout(() => (this.invalidMsg = ""), 2500);
    },
    nextRound() {
      this.is_round_over = false;
      this.round++;
      this.word = this.words[this.round - 1];
      this.letterArray = [[], [], [], [], [], []];
      this.$refs.keyboardRef.reset();
      this.rightSpot = [];
      this.rightLetter = [];
      this.greenKey = [];
      this.yellowKey = [];
      this.grayKey = [];
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
  background-color: white;
}
button:hover {
  background-color: rgb(12, 164, 30);
  color: white;
  cursor: pointer;
}
.invalid-word {
  color: red;
}
</style>

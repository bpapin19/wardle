<template>
  <div :class="keyboardClass"></div>
</template>

<script>
import Keyboard from "simple-keyboard";
import "simple-keyboard/build/css/index.css";
import axios from "axios";

export default {
  name: "SimpleKeyboard",
  props: {
    keyboardClass: {
      default: "simple-keyboard",
      type: String,
    },
    input: {
      type: String,
    },
    greenKey: Array,
    yellowKey: Array,
    grayKey: Array,
  },
  watch: {
    greenKey: {
      deep: true,
      handler: function (newValue) {
        this.keyboard.setOptions({
          buttonTheme: [
            {
              class: "hg-green",
              buttons: newValue.join(" ").toUpperCase(),
            },
            {
              class: "hg-yellow",
              buttons: this.yellowKey.join(" ").toUpperCase(),
            },
            {
              class: "hg-gray",
              buttons: this.grayKey.join(" ").toUpperCase(),
            },
          ],
        });
      },
    },
    yellowKey: {
      deep: true,
      handler: function (newValue) {
        this.keyboard.setOptions({
          buttonTheme: [
            {
              class: "hg-green",
              buttons: this.greenKey.join(" ").toUpperCase(),
            },
            {
              class: "hg-yellow",
              buttons: newValue.join(" ").toUpperCase(),
            },
            {
              class: "hg-gray",
              buttons: this.grayKey.join(" ").toUpperCase(),
            },
          ],
        });
      },
    },
    grayKey: {
      deep: true,
      handler: function (newValue) {
        this.keyboard.setOptions({
          buttonTheme: [
            {
              class: "hg-green",
              buttons: this.greenKey.join(" ").toUpperCase(),
            },
            {
              class: "hg-yellow",
              buttons: this.yellowKey.join(" ").toUpperCase(),
            },
            {
              class: "hg-gray",
              buttons: newValue.join(" ").toUpperCase(),
            },
          ],
        });
      },
    },
  },
  data: () => ({
    keyboard: null,
    word: "",
    row: 0,
  }),
  mounted() {
    this.keyboard = new Keyboard(this.keyboardClass, {
      onChange: this.onChange,
      onKeyPress: this.onKeyPress,
      theme: "hg-theme-default hg-layout-default myTheme",
      layout: {
        default: [
          "Q W E R T Y U I O P",
          "A S D F G H J K L",
          "{bksp} Z X C V B N M {enter}",
        ],
      },
      display: {
        "{bksp}": "back",
        "{enter}": "enter",
      },
      buttonTheme: [
        {
          class: "hg-green",
          buttons: this.greenKey.join(" ").toUpperCase(),
        },
      ],
    });
  },
  methods: {
    onKeyPress(button) {
      this.$emit("onKeyPress", button);

      var letters = /^[a-zA-Z]+$/;
      if (this.word.length < 5 && button.match(letters)) {
        this.$emit("fill-tile", button, this.row);
        this.word += button;
      }

      if (button === "{bksp}") {
        this.word = this.word.substring(0, this.word.length - 1);
        this.$emit("backspace", this.row);
      }

      if (button === "{enter}" && this.word.length === 5) {
        axios
          .get(`https://api.dictionaryapi.dev/api/v2/entries/en/${this.word}`)
          .then(() => {
            this.$emit("check-word", this.word.toLowerCase(), this.row);
            this.word = "";
            this.row += 1;
          })
          .catch(() => {
              console.log("faile")
            this.$emit("invalid-word", this.word.toLowerCase());
          });
      }
    },
    reset() {
      this.word = "";
      this.row = 0;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.simple-keyboard.hg-layout-default .hg-button.hg-green {
  background: green;
  color: white;
}
.simple-keyboard.hg-layout-default .hg-button.hg-yellow {
  background: #b59f3a;
  color: white;
}
.simple-keyboard.hg-layout-default .hg-button.hg-gray {
  background: rgb(50, 50, 50);
  color: white;
}
</style>

<template>
  <div :class="keyboardClass"></div>
</template>

<script>
import Keyboard from "simple-keyboard";
import "simple-keyboard/build/css/index.css";

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
    });
  },
  methods: {
    onChange(input) {
      this.$emit("onChange", input);
    },
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
        this.$emit("check-word", this.word, this.row);
        this.word = "";
        this.row += 1;
      }
    },
    reset() {
      this.word = "";
      this.row = 0;
    },
    handleShift() {
      let currentLayout = this.keyboard.options.layoutName;
      let shiftToggle = currentLayout === "default" ? "shift" : "default";

      this.keyboard.setOptions({
        layoutName: shiftToggle,
      });
    },
  },
  watch: {
    input(input) {
      this.keyboard.setInput(input);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.visible {
  
}
.hidden {
  
}
</style>

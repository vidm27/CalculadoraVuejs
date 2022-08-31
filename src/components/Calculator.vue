<template>
  <div class="container calculator">
    <div class="theme">
      <span>Calc</span>
    </div>
    <div class="promt">
      <span class="promt__text">{{ prompt }}</span>
    </div>
    <div class="calculator__keyboard">
      <div class="keyboard__grid">
        <button
          v-for="btnKey of cal_keyboard"
          :key="btnKey.id"
          :value="btnKey.value"
          @click="evalueteKeyPress(btnKey)"
        >
          {{ btnKey.text }}
        </button>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "Calculator",
  data() {
    return {
      prompt: "",
      previus_press: "",
      cal_keyboard: [
        { id: "7", text: "7", value: "7", class: "number" },
        { id: "8", text: "8", value: "8", class: "number" },
        { id: "9", text: "9", value: "9", class: "number" },
        { id: "del", text: "del", value: "del", class: "del" },
        { id: "4", text: "4", value: "4", class: "number" },
        { id: "5", text: "5", value: "5", class: "number" },
        { id: "6", text: "6", value: "6", class: "number" },
        { id: "plus", text: "+", value: "+", class: "symbol" },
        { id: "1", text: "1", value: "1", class: "number" },
        { id: "2", text: "2", value: "2", class: "number" },
        { id: "3", text: "3", value: "3", class: "number" },
        { id: "minus", text: "-", value: "-", class: "symbol" },
        { id: "decimal", text: ".", value: ".", class: "symbol" },
        { id: "0", text: "0", value: "0", class: "number" },
        { id: "divide", text: "/", value: "/", class: "symbol" },
        { id: "multiplication", text: "x", value: "x", class: "symbol" },
        { id: "reset", text: "reset", value: "reset", class: "reset" },
        { id: "equal", text: "=", value: "=", class: "equal" },
      ],
    };
  },
  methods: {
    evalueteKeyPress(keyboard) {
      if (keyboard.class === "reset") {
        this.prompt = "";
      } else if (keyboard.class === "del") {
        const last_chart = this.prompt.length;
        this.prompt = this.prompt.substring(0, last_chart - 1);
      }

      if(keyboard.value === "x"){
        keyboard.value = "*";
      }

      console.log(keyboard.class);
      if (this.previus_press === "") {
        this.previus_press = keyboard.class;
        this.prompt = keyboard.value;
      } else if (
        this.previus_press === "number" &&
        keyboard.class === "number"
      ) {
        this.prompt += keyboard.value;
        this.previus_press = keyboard.class;
      } else if (
        this.previus_press === "number" &&
        keyboard.class === "symbol"
      ) {
        this.prompt += keyboard.value;
        this.previus_press = keyboard.class;
      } else if (
        this.previus_press === "symbol" &&
        keyboard.class === "number"
      ) {
        this.prompt += keyboard.value;
        this.previus_press = keyboard.class;
      }

      if(keyboard.class === "equal"){
        const result = Function("return " + this.prompt)();
        this.prompt = result;
      }
    },
  },
};
</script>
<style scoped>
</style>

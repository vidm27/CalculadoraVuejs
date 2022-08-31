<template>
  <div class="container calculator">
    <div class="theme">
      <span>Calc</span>
    </div>
    <div class="prompt">
      <span class="prompt__text">{{ prompt }}</span>
    </div>
    <div class="calculator__keyboard">
      <div class="keyboard__grid">
        <button
          class="key"
          v-for="btnKey of cal_keyboard"
          :key="btnKey.id"
          :value="btnKey.value"
          :class="{ del: btnKey.class === 'del' }"
          @click="evalueteKeyPress(btnKey)"
        >
          {{ btnKey.text }}
        </button>
        <button class="key del reset">reset</button>
        <button class="key equal">=</button>
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
      ],
    };
  },
  methods: {
    evalueteKeyPress(keyboard) {
      if (keyboard.class === "reset") {
        this.prompt = "";
      } else if (keyboard.class === "del") {
        const last_chart = this.prompt.length;
        if (last_chart === 0) {
          this.prompt = "";
          return;
        }
        this.prompt = this.prompt.substring(0, last_chart - 1);
      }

      if (keyboard.value === "x") {
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
    },
  },
};
</script>
<style scoped>
.container.calculator {
  width: 80%;
  max-width: 550px;
  margin: 0 auto;
}
.prompt {
  background: var(--bg-promt-default-color);
  height: 6rem;
  border-radius: 0.7rem;
  text-align: right;
  color: var(--color-default-text-alternative);
  padding: 1rem 1.5rem;
  box-sizing: border-box;
  display: flex;
  align-items: center;
  justify-content: flex-end;
  align-content: center;
  margin-bottom: 1rem;
}
.prompt .prompt__text {
  font-size: 3em;
  font-weight: bold;
}
.calculator__keyboard {
  background: #242d44;
  padding: 1rem 1.5rem;
  border-radius: 0.7rem;
}
.calculator__keyboard .keyboard__grid {
  display: grid;
  gap: 1.5rem;
  grid-template-columns: repeat(4, 1fr);
}
.keyboard__grid .key {
  border: 0;
  height: 3rem;
  font-size: 2rem;
  font-weight: bold;
  color: #434a59;
  border-radius: 0.5rem;
  text-transform: uppercase;
  text-align: center;
  box-shadow: #b3a497 0px 6px 0px;
}
.keyboard__grid .key:hover {
  background: #ffffff;
  box-shadow: #B3A497 0px 6px 0px;
}
.keyboard__grid .key.del {
  background: #647198;
  color: #fff;
  font-size: 1.3rem;
  box-shadow: #414e73 0px 6px 0px;
}
.keyboard__grid .key.del:hover {
  background: #A2B2E1;
  box-shadow: #414E73 0px 6px 0px;
}
.keyboard__grid .key.reset {
  grid-column-end: span 2;
}
.keyboard__grid .key.equal {
  grid-column-end: span 2;
  background: #d03f2f;
  color: #fff;
  font-size: 1.5rem;
  box-shadow: #93261a 0px 6px 0px;
}
.keyboard__grid .key.equal:hover{
  background: #F96B5B;
}
</style>

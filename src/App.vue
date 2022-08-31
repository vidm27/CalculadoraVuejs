<template>
  <Calculator></Calculator>
</template>

<script>
import Calculator from './components/Calculator.vue'

export default {
  name: 'App',
  components: {
    Calculator
  }
}
</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=League+Spartan:wght@300;400;700&display=swap');
:root{
  --bg-default-color: #3A4663;
  --bg-promt-default-color: #181F33;
  --bg-button-default-color: #EAE3DC;
  --bg-button-equal-default-color: #D03F2F;
  --bg-button-delete-default-color: #647198;
  --color-default-text-keyboard: #434A59;
  --color-default-text-alternative: #ffffff;
}
body{
  padding: 0;
  margin: 0;
  background: var(--bg-default-color);
  font-family: 'League Spartan', sans-serif;
}
</style>

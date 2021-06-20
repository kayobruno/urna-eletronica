<template>
  <div class="keyboard">
    <div class="numeric">
      <div class="line">
        <button v-on:click="addNumber(1)">1</button>
        <button v-on:click="addNumber(2)">2</button>
        <button v-on:click="addNumber(3)">3</button>
      </div>

      <div class="line">
        <button v-on:click="addNumber(4)">4</button>
        <button v-on:click="addNumber(5)">5</button>
        <button v-on:click="addNumber(6)">6</button>
      </div>

      <div class="line">
        <button v-on:click="addNumber(7)">7</button>
        <button v-on:click="addNumber(8)">8</button>
        <button v-on:click="addNumber(9)">9</button>
      </div>

      <div class="line">
        <button v-on:click="addNumber(0)">0</button>
      </div>
    </div>

    <div class="actions">
      <button class="btn-white" v-on:click="voteNull">BRANCO</button>
      <button class="btn-correct" v-on:click="correct">CORRIGIR</button>
      <button class="btn-confirm" v-on:click="confirm">CONFIRMAR</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Keyboard',
  props: {
    addNumber: Function,
    correct: Function,
    confirm: Function,
    voteNull: Function,
  }
}
</script>

<style>
.keyboard {
  width: 40%;
  height: 100%;
  background-color: var(--ballot-box-keyboard-color);
  border-radius: 5px;
  padding: 20px;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
}

.numeric {
  width: 100%;
}

.numeric .line {
  display: flex;
  justify-content: space-around;
  margin-bottom: 20px;
}

.numeric button {
  background-color: var(--ballot-box-keyboard-button-color);
  color: var(--light-text-color);
  font-size: 30px;
  border-radius: 5px;
  width: 80px;
  height: 50px;
}

.actions {
  width: 100%;
  display: flex;
  justify-content: space-around;
}

.actions button {
  color: var(--dark-text-color);
  font-size: 15px;
  border-radius: 5px;
  width: 30%;
  height: 50px;
}

.btn-white {
  background-color: var(--ballot-box-white-button-color);
}

.btn-correct {
  background-color: var(--ballot-box-correct-button-color);
}

.btn-confirm {
  background-color: var(--ballot-box-confirm-button-color);
}
</style>
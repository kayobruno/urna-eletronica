<template>
  <div id="app">
    <div class="urna">
      <Screen 
        :step="step"
        :voteNumber="voteNumber"
        :numberQty="numberQty"
        :currentCandidate="currentCandidate"
       />

      <Keyboard 
        :addNumber="addNumber"
        :correct="correct"
        :confirm="confirm"
        :voteNull="voteNull"
      />
    </div>
  </div>
</template>

<script>

import '@/css/global.css'
import Keyboard from '@/components/Keyboard'
import Screen from '@/components/Screen'

import confirmAudio from '@/assets/audios/confirm.wav'
import keyAudio from '@/assets/audios/key.wav'

export default {
  name: 'App',
  components: {
    Keyboard,
    Screen
  },
  methods: {
    addNumber(number) {
      this.runAudio(keyAudio)

      if (this.voteNumber.length === this.numberQty) return
      this.voteNumber += number

      this.checkCandidate();
    },

    checkCandidate() {
      if (this.voteNumber.length < this.numberQty) return false

      if (this.candidates[this.step][this.voteNumber]) {
        this.currentCandidate = this.candidates[this.step][this.voteNumber]
        return true
      }

      this.currentCandidate = {
        nome: 'Voto Nulo',
        partido: 'Voto Nulo',
        imagem: '',
      }
    },

    correct() {
      this.clear()
    },

    clear() {
      this.currentCandidate = {}
      this.voteNumber = ''
    },

    confirm() {
      if (this.voteNumber.length < this.numberQty) return false
      this.nextStep()
    },

    nextStep() {
      this.runAudio(confirmAudio)

      if (this.step == 'prefeito') {
        this.step = 'vereador'
        this.numberQty = 5
        return this.clear()
      }

      this.step = 'fim'

      let instancy = this

      setTimeout(function() {
        instancy.step = 'prefeito'   
        instancy.numberQty = 2
        return instancy.clear()     
      }, 3000)
    },

    voteNull() {
      if (this.step === 'fim') return false

      this.clear()
      this.nextStep()
    },

    runAudio(audio) {
      if (audio) {
        let currentAudio = new Audio(audio)
        currentAudio.play()
      }
    }
  },

  data() {
    return {
      step: 'prefeito',
      voteNumber: '',
      numberQty: 2,
      currentCandidate: {},
      candidates: {
        "prefeito":{
          "01":{
            "nome": "Ash",
            "partido": "Pokemon",
            "imagem": "https://raw.githubusercontent.com/william-costa/wdev-urna-eletronica-resources/master/images/ash.png"
          },
          "08":{
            "nome": "Vegeta",
            "partido": "Dragon Ball",
            "imagem": "https://raw.githubusercontent.com/william-costa/wdev-urna-eletronica-resources/master/images/vegeta.png"
          }
        },
        "vereador":{
          "01234":{
            "nome": "Pikachu",
            "partido": "Pokemon",
            "imagem": "https://raw.githubusercontent.com/william-costa/wdev-urna-eletronica-resources/master/images/pikachu.png"
          },
          "08001":{
            "nome": "Goku",
            "partido": "Dragon Ball",
            "imagem": "https://raw.githubusercontent.com/william-costa/wdev-urna-eletronica-resources/master/images/goku.png"
          }
        }
      },
    }
  }
}
</script>

<style>
#app {
  background-color: var(--background-color);
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.urna {
  width: 1000px;
  height: 500px;
  background-color: var(--ballot-box-background-color);
  padding: 30px;
  border-radius: 5px;
  display: flex;
  justify-content: space-around;
}
</style>

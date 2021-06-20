<template>
  <div class="screen-container">
    <div v-if="step !== 'fim'" class="vote">
      <div class="vote-text">
        <div class="vote-title">
            Seu voto para:
        </div>
        
        <div class="vote-type">
            {{ step }}
        </div>

        <div class="vote-number">
            Números
            <div class="number" v-for="(value, key) in voteNumber.padEnd(numberQty, ' ')" :key="key">
                {{ value }}
            </div>
        </div>

        <div class="vote-description">
          Nome: <strong>{{ currentCandidate.nome ? currentCandidate.nome : '___________' }}</strong>
        </div>

        <div class="vote-description">
          Partido: <strong>{{ currentCandidate.partido ? currentCandidate.partido : '___________' }}</strong>
        </div>
      </div>

      <div v-if="currentCandidate.imagem" class="vote-image">
        <img :src="currentCandidate.imagem" />
      </div>

      <div class="vote-instructions">
        <p>Aperte a tecla:</p>
        <p><strong>BRANCA</strong> para <strong>VOTAR</strong> EM <strong>BRANCO</strong></p>
        <p><strong>LARANJA</strong> para <strong>CORRIGIR</strong></p>
        <p><strong>VERDE</strong> para <strong>CONFIRMAR</strong></p>
      </div>
    </div>

    <div v-if="step === 'fim'" class="end">
      FIM
    </div>
  </div>
</template>

<script>
export default {
  name: 'Screen',
  props: {
    step: String,
    voteNumber: String,
    numberQty: Number,
    currentCandidate: Object,
  }
}
</script>

<style>
.screen-container {
  width: 55%;
  height: 100%;
  background-color: var(--ballot-box-screen-color);
  border-radius: 5px;
  border: 2px solid var(--light-border-color);
  padding: 20px;
  color: var(--dark-text-color);
}

.vote-title {
  font-size: 20px;
}

.vote-type {
  font-size: 30px;
  font-weight: bold;
  margin: 20px 0;
  text-transform: uppercase;
}

.vote-number {
  display: flex;
  align-items: center;
}

.number {
  width: 45px;
  height: 55px;
  border: 1px solid var(--dark-border-color);
  margin-left: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 30px;
}

.vote-description {
  margin-top: 20px;
}

.vote-image img{
  width: 110px;
  height: 150px;
  border: 1px solid var(--dark-border-color);
}

.vote {
  display: flex;
  flex-wrap: wrap;
  width: 100%;
  height: 100%;
}

.vote-text {
  flex: 1;
}

.vote-instructions {
  width: 100%;
  border-top: 1px solid var(--dark-border-color);
  font-size: 13px;
  margin-top: 20px;
  padding-top: 10px;
}

.end {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100%;
  font-size: 120px;
}
</style>
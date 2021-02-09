<template>
<div>
  <h1>Ninja Reaction Timer</h1>
  <button @click="start" :disabled="isPlaying">Play</button>
  <!-- su binding paima is apacios kur data funkcija yra -->
  <Block v-if="isPlaying" :delay="delay" @end="endGame" />
  <!-- <p v-if="showResults">Reaction time: {{ score }} ms</p> -->
  <Results v-if="showResults" :score="score" />
</div>
</template>

<script>
// challenge
// - when the game ends, show the results component
// - output the score inside the results component

import Block from './components/Block.vue';
import Results from './components/Results.vue';

export default {
  name: 'App',
  // kai importuoji reikia tada uzregistruoti komponentus tai kitus failus
  components: { Block, Results },
  // data tai function kuri grazina objekta
  data() {
    return {
      // cia yra viduje objekto todel yra objekto reiksmes sudetos name: value
      isPlaying: false,
      delay: null,
      score: null,
      showResults: false
    }
  },
  methods: {
    start() {
      // grynai objektinis programavinas nes kreipiesi i vidu nurodydamas this
      // cia nurodo kad random reiksme ims didziausia trukme gali buti 7s arba maziauria 2s
      this.delay = 2000 + Math.random() * 5000;
      this.isPlaying = true;
      this.showResults = false;
      // console.log(this.delay);
    },
    endGame(reationTime) {
      // store this time in variable into data() {} function
      this.score = reationTime;
      this.isPlaying = false;
      this.showResults = true;
      // tai kas cia vyksta tai tiesiog i score ideda laika su $emit is Block.vue failo
      // sugeneruota laika, tada ji ideda i kintamaji score. ir ji atspindi virsuje paragrafe Reaction time
    }
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #444;
  margin-top: 60px;
}

button {
  background-color: #0faf87;
  color: white;
  border: none;
  padding: 8px 16px;
  border-radius: 4px;
  font-size: 16px;
  letter-spacing: 1px;
  cursor: pointer;
  margin: 10px;
}

button:disabled {
  opacity: 0.2;
  cursor: not-allowed;
}

</style>

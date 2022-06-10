<template>
  <div class="container" @click.self="tooEarly">
    <h1>Reaction Timer</h1>
    <button @click="start" :disabled="isPlaying">Play</button>
    <Block v-if="isPlaying" :delay="delay" @end="endGame" />
    <Results v-if="showResults" :score="score" />
    <p class="error" v-if="showError">Too early! Try again...</p>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import Block from "./components/Block.vue";
import Results from "@/components/Results.vue";

export default defineComponent({
  name: "App",
  components: {
    Block,
    Results,
  },
  data: () => ({
    isPlaying: false,
    delay: 0,
    score: 0,
    showResults: false,
    showError: false,
  }),
  methods: {
    start() {
      this.delay = 2000 + Math.random() * 5000;
      this.isPlaying = true;
      this.showResults = false;
      this.showError = false;
    },
    endGame(reactionTime: number) {
      this.score = reactionTime;
      this.isPlaying = false;
      this.showResults = true;
    },
    tooEarly() {
      if (this.isPlaying) this.showError = true;
      this.isPlaying = false;
    },
  },
});
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #444;
  margin-top: 60px;
}
h1 {
  margin: 20px 0;
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
button[disabled] {
  opacity: 0.2;
  cursor: not-allowed;
}
.container {
  width: 100%;
  height: calc(100vh - 80px);
}
.error {
  font-size: 1.4em;
  color: #0faf87;
  font-weight: bold;
}
</style>

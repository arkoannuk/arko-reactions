<template>
  <div class="container py-4 px-3 mx-auto text-center">
    <h1 class="mt-5">Reaction Timer</h1>
    <button
      type="button"
      class="btn btn-primary mt-3"
      :disabled="btnDisable"
      @click="toggleBlock"
    >
      Play Game
    </button>
    <div v-show="showBlock">
      <GameBlock @click="logTime" />
    </div>
    <div v-show="showResult">
      <Results :timeTaken="timeTaken" />
    </div>
  </div>
</template>

<script>
import GameBlock from "./components/GameBlock.vue"
import Results from "./components/Results.vue"

export default {
  name: "App",
  components: {
    GameBlock,
    Results,
  },
  data() {
    return {
      showBlock: false,
      showResult: false,
      btnDisable: false,
      randomDuration: null,
      startTime: null,
      timeTaken: null,
    }
  },
  methods: {
    toggleBlock() {
      this.btnDisable = !this.btnDisable
      this.randomDuration = Math.floor(Math.random() * (3500 - 1000 + 1)) + 1000

      if (this.timeTaken) {
        this.showResult = !this.showResult
      }

      setTimeout(
        () => {
          this.showBlock = !this.showBlock
          this.startTime = Date.now()
        },
        this.showBlock ? 0 : this.randomDuration
      )
    },

    logTime() {
      this.timeTaken = Date.now() - this.startTime
      this.showResult = !this.showResult
      this.showBlock = !this.showBlock
      this.btnDisable = !this.btnDisable
    },
  },
}
</script>

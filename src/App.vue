<script>
import MainScreenVue from './views/MainScreen.vue'
import GamePlayScreenVue from './views/GamePlayScreen.vue'
import ResultScreenVue from './views/ResultScreen.vue'

import { suffled } from './utils/array.ts'

export default {
  name: 'App',
  data() {
    return {
      settings: {
        totalBlocks: 0,
        cardsContext: [],
        startedAt: null
      },
      statusMatch: 'default',
      timer: 0
    }
  },
  components: {
    MainScreenVue,
    GamePlayScreenVue,
    ResultScreenVue
  },
  methods: {
    getResult() {
      this.timer = new Date().getTime() - this.settings.startedAt

      this.statusMatch = 'result'
    },
    onStartAgain() {
      this.statusMatch = 'default'
    },
    onHandleBeforeStart(config) {
      this.settings.totalBlocks = config

      const cardPairs = Array.from({ length: this.settings.totalBlocks / 2 }, (_, i) => i + 1)

      const cards = [...cardPairs, ...cardPairs]

      this.settings.cardsContext = suffled(suffled(cards))

      this.statusMatch = 'play'

      this.settings.startedAt = new Date().getTime()
    }
  }
}
</script>

<template>
  <MainScreenVue v-if="statusMatch === 'default'" @onStart="onHandleBeforeStart($event)" />
  <GamePlayScreenVue
    v-if="statusMatch === 'play'"
    :cardsContext="settings.cardsContext"
    @onFinish="getResult()"
  />
  <ResultScreenVue :timer="timer" v-if="statusMatch === 'result'" @onStartAgain="onStartAgain()" />
</template>

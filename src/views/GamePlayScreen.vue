<template>
  <div class="center game-play">
    <div class="game-play__container">
      <CardPlay
        v-for="(card, index) in cardsContext"
        :key="'card' + index"
        :ref="`card-${index}`"
        :imgBack="{ card, index }"
        @onFlip="checkRule($event)"
      />
    </div>
    <CopyRight />
  </div>
</template>
<style>
.game-play {
  height: 100vh;
}
.game-play__container {
  margin-top: 40px;
  display: inline-grid;
  gap: 20px;
}
</style>
<script>
import CardPlay from '@/components/CardPlay.vue'
import CopyRight from '@/components/CopyRight.vue'

export default {
  props: {
    cardsContext: {
      type: Array,
      default: function () {
        return []
      }
    }
  },
  components: {
    CardPlay,
    CopyRight
  },
  created() {
    this.load()
  },
  data() {
    return {
      rules: [],
      activePairs: 0
    }
  },
  methods: {
    load() {
      this.$nextTick(() => {
        const container = document.querySelector('.game-play__container')
        if (container) {
          container.style.gridTemplateColumns = `repeat(${Math.sqrt(
            this.cardsContext.length
          )}, 1fr)`
        }
      })
    },
    checkRule(card) {
      if (this.rules.length < 2) {
        this.rules.push(card)
        this.$refs[`card-${card.index}`][0].setAcTived()
      }

      if (this.rules.length === 2 && this.rules[0]?.card === this.rules[1]?.card) {
        this.activePairs = this.activePairs + 1

        this.rules = []

        if (this.activePairs === this.cardsContext.length / 2) {
          setTimeout(() => {
            this.$emit('onFinish')
          }, 1000)
        }
      } else if (this.rules.length === 2 && this.rules[0]?.card !== this.rules[1]?.card) {
        const indexS = [this.rules[0].index, this.rules[1].index]
        this.rules = []
        setTimeout(() => {
          this.$refs[`card-${indexS[0]}`][0].onFlipBack()
          this.$refs[`card-${indexS[1]}`][0].onFlipBack()
        }, 500)
      } else {
        return false
      }
    }
  }
}
</script>

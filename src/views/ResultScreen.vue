<template>
  <div class="result center">
    <div class="result__container">
      <h2 class="result__title">✨ Congratulations ✨</h2>
      <p class="result__timer">
        <span>
          {{ Math.round((timer - 1000) / 1000) }}
        </span>
        seconds
      </p>
      <button class="result__play-agin-button" @click="startAgain()">Start again</button>
      <CopyRight />
    </div>
  </div>
</template>

<script>
import CopyRight from '@/components/CopyRight.vue'

export default {
  name: 'ResultScreen',
  components: {
    CopyRight
  },
  props: {
    timer: {
      type: Number
    }
  },
  methods: {
    startAgain() {
      this.$emit('onStartAgain')
    }
  }
}
</script>

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

<style>
.result {
  margin: 40px 0;
  height: 100vh;
}
.result__container {
  text-align: center;
}
.result__title {
  font-size: 72px;
  color: var(--light);
  margin-bottom: 20px;
}
.result__timer {
  color: var(--light);
  font-size: 32px;
  margin-bottom: 30px;
}
.result__timer > span {
  color: var(--primary);
}
.result__play-agin-button {
  font-size: 20px;
  padding: 16px 24px;
  background-color: transparent;
  border: 1px solid var(--light);
  color: var(--light);
  font-family: var(--font);
  border-radius: 8px;
  cursor: pointer;
}
</style>

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

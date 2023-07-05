<script>
import CopyRight from '@/components/CopyRight.vue'

export default {
  name: 'MainScreen',
  components: {
    CopyRight
  },
  methods: {
    onStart(totalBlocks) {
      this.$emit('onStart', totalBlocks)
    }
  }
}
</script>
<template>
  <div class="main">
    <div>
      <h1 class="main__title">POKE MEMORIES</h1>
      <p class="main__description">Select mode to start a game</p>
      <div class="main__actions">
        <button @click="onStart(4)">
          <span class="main__actions_title">2x2</span>
          <span>Easy</span>
        </button>
        <button @click="onStart(16)">
          <span class="main__actions_title">4x4</span>
          <span>Normal</span>
        </button>
        <button @click="onStart(36)">
          <span class="main__actions_title">6x6</span>
          <span>Medium</span>
        </button>
        <button @click="onStart(64)">
          <span class="main__actions_title">8x8</span>
          <span>Hard</span>
        </button>
      </div>
      <CopyRight />
    </div>
  </div>
</template>

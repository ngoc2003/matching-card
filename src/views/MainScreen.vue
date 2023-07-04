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
        <button @click="onStart(100)">
          <span class="main__actions_title">10x10</span>
          <span>Advanced</span>
        </button>
        <button @click="onStart(144)">
          <span class="main__actions_title">12x12</span>
          <span>Legend</span>
        </button>
      </div>
      <CopyRight />
    </div>
  </div>
</template>

<style>
.main {
  padding: 40px 40px 0;
  display: grid;
  place-items: center;
  min-height: 100vh;
}
.main > div {
  text-align: center;
}
.main__title {
  font-size: 72px;
  color: var(--light);
  padding-bottom: 10px;
}
.main__description {
  font-size: 28px;
  color: var(--light);
  padding-bottom: 20px;
}
.main__actions {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 40px;
}
.main__actions button {
  transition: cubic-bezier(0.075, 0.82, 0.165, 1) 0.2s;
  overflow: hidden;
  cursor: pointer;
  background-color: transparent;
  border: 1px solid var(--light);
  color: var(--light);
  border-radius: 16px;
  height: 150px;
  width: 150px;
}
.main__actions button:hover {
  background-color: var(--light);
  color: var(--dark);
}
.main__actions button span {
  display: block;
  font-family: var(--font);
}
.main__actions_title {
  font-size: 28px;
  margin-bottom: 10px;
}
.main__actions button span:not(.main__actions_title) {
  font-size: 20px;
}
</style>

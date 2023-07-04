<template>
  <div class="card">
    <div
      class="card__inner"
      :class="{ flipped: isFlipped, active: isActive }"
      @click="onToggleCard()"
    >
      <div class="card__face card__face--font">
        <div class="card__content"></div>
      </div>
      <div class="card__face card__face--back">
        <div
          class="card__content"
          :style="{ background: `url(${imageURL}) center center/ contain no-repeat` }"
        ></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    imgBack: {
      card: {
        type: Number
      },
      index: {
        type: Number
      }
    }
  },
  data() {
    return {
      isActive: false,
      isFlipped: false,
      imageLoaded: false,
      imageURL: null
    }
  },
  created() {
    this.loadImage()
  },
  methods: {
    onFlipBack() {
      this.isFlipped = false
      this.setUnActive()
    },
    async loadImage() {
      const imageModule = await import(`../assets/images/${this.imgBack.card}.png`)
      this.imageURL = imageModule.default
      this.imageLoaded = true
    },
    onToggleCard() {
      this.isFlipped = !this.isFlipped
      if (this.isFlipped) {
        this.$emit('onFlip', this.imgBack)
      }
    },
    setAcTived() {
      this.isActive = true
    },
    setUnActive() {
      this.isActive = false
    }
  }
}
</script>

<style>
.card {
  display: inline-block;
  margin-right: 1rem;
  margin-bottom: 1rem;
  width: 90px;
  height: 120px;
}

.card__inner {
  width: 100%;
  height: 100%;
  transition: transform 0.5s;
  transform-style: preserve-3d;
  cursor: pointer;
  position: relative;
}

.card__content {
  width: 100%;
  height: 100%;
}

.card__face--font .card__content {
  background: url('../assets/images/icon_back.png') center center/contain no-repeat;
}

.card__inner.flipped {
  transform: rotateY(-180deg);
}

.card__inner.active {
  cursor: default;
  pointer-events: none;
}

.card__face {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  overflow: hidden;
  border-radius: 1rem;
  padding: 1rem;
  box-shadow: 0 3px 10px 3px rgba(0, 0, 0, 0.3);
}

.card__face--back {
  background-color: var(--light);
  transform: rotateY(-180deg);
}
</style>

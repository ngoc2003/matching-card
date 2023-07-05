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

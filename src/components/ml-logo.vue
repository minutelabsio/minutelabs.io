<template lang="pug">
.ml-logo
  img(width="160", src="//cdn.minutelabs.io/logos/logo-minutelabs-off.jpg", alt="MinuteLabs.io")
  img.flicker(v-show="flicker", width="160", src="//cdn.minutelabs.io/logos/logo-minutelabs-on.jpg")
</template>

<script>
export default {
  name: 'ml-logo'
  // , props: {
  // }
  , data: () => ({
    flicker: false
    , timeout: null
  })
  , components: {
  }
  , mounted(){
    // preload
    this.initLogoFlicker()
  }
  , destroyed(){
    clearTimeout(this.timeout)
  }
  // , computed: {
  // }
  , methods: {
    initLogoFlicker(){
      var light = this.$el
      if (!light) { return }

      this.flicker = true

      setTimeout(() => {
        this.flicker = false
      }, 1400)

      var randomDelay = (((Math.random() * 6) | 0) + 10) * 1000
      this.timeout = setTimeout(() => this.initLogoFlicker(), randomDelay)
    }
  }
}
</script>

<style lang="sass" scoped>
@import '@/styles/_variables.scss'
@keyframes flickerAnimation
  0%
    opacity: 1
  10%
    opacity: 0
  15%
    opacity: 1
  30%
    opacity: 0
  50%
    opacity: 1
  55%
    opacity: 0
  68%
    opacity: 1
  79%
    opacity: 0
  90%
    opacity: 1
  98%
    opacity: 0

.ml-logo
  position: relative
  width: 160px

  &,
  img
    display: block
    margin: auto

    &.flicker
      display: block
      position: absolute
      top: 0
      left: 0
      right: 0
      bottom: 0
      max-width: none
      animation: flickerAnimation 0.8s infinite cubic-bezier(0,1,0,1)
</style>

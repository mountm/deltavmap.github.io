<template>
  <div class="map-banner-container"
       :class="[(fadeAway) ? 'fade-away' : '']"
       v-if="displayBanner"
  >
    <div class="map-banner">
      <slot></slot>
      <button type="button"
              @click="handleClose"
      >close</button>
    </div>
  </div>
</template>
<script>
export default {
  data () {
    const bannerTitle = 'banner-intro-hide'
    const introHide = localStorage.getItem(bannerTitle)
    return {
      bannerTitle,
      fadeAway: false,
      displayBanner: introHide !== 'true'
    }
  },
  methods: {
    handleClose: function () {
      this.fadeAway = true
      localStorage.setItem(this.bannerTitle, 'true')
      setTimeout(_ => {
        this.displayBanner = false
      }, 250)
    }
  }
}
</script>
<style lang="sass">
@import '@/sass/variables'
.map-banner
  background-color: $color-map-dark
  border-radius: .5em
  color: $color-map-light
  display: flex
  justify-content: space-between
  max-width: 400px
  padding: .5em 1em

  button
    color: hotpink
    font-size: .8em
    letter-spacing: .12em
    margin-left: .5rem
    text-transform: uppercase

  &-container
    grid-column-start: 2
    grid-column-end: 2
    grid-row-start: 1
    grid-row-end: 1
    box-sizing: border-box
    margin: 0 auto
    position: relative
    height: 0
    top: 1rem
    z-index: 2
    opacity: 1
    transition: all .25s

    @media #{map-get($display-breakpoints, 'sm-and-down')}
      grid-column-start: 1
      grid-column-end: 1
      grid-row-start: 2
      grid-row-end: 2

    &.fade-away
      opacity: 0

</style>

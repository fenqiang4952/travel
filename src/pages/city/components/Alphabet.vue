<template>
  <ul class="list">
    <li class="item" v-for="item of letters" :key="item" :ref="item" @click="handleClick(item)"
      @touchstart.prevent="handleTouchStart"
      @touchmove="handleTouchMove"
      @touchend="handleTouchEnd">
      {{item}}
    </li>
  </ul>
</template>

<script>
export default {
  name: 'CityAlphabet',
  props: {
    cities: Object
  },
  data () {
    return {
      touchStatus: false,
      startY: 0,
      timer: null
    }
  },
  computed: {
    letters () {
      return Object.keys(this.cities)
    }
  },
  updated () {
    this.startY = this.$refs['A'][0].offsetTop
  },
  methods: {
    handleClick (key) {
      this.$emit('change', key)
    },
    handleTouchStart () {
      this.touchStatus = true
    },
    handleTouchMove (e) {
      if (this.touchStatus) {
        if (this.timer) {
          clearTimeout(this.timer)
          this.timer = null
        }
        this.timer = setTimeout(() => {
          const touchY = e.touches[0].clientY - this.startY - 79
          const index = Math.floor(touchY / 20)
          if (index >= 0 && index < this.letters.length) {
            this.$emit('change', this.letters[index])
          }
        }, 16)
      }
    },
    handleTouchEnd () {
      this.touchStatus = false
    }
  }
}
</script>

<style lang="stylus" scoped>
  @import '~@styles/varibles.styl'
  .list
    display flex
    flex-direction column
    justify-content center
    align-items center
    position absolute
    right 0
    top 1.58rem
    bottom 0
    width .4rem
    .item
      line-height .4rem
      color $bgColor

</style>

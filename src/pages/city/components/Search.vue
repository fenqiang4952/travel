<template>
  <div>
    <div class="search">
      <input v-model="keyword" class="search-input" type="text" placeholder="输入城市名或拼音" />
    </div>
    <div class="serach-content" v-show="keyword" ref="wrapper">
      <ul>
        <li class="search-item border-bottom" @click="handleCityClick(item.name)" v-for="(item) in list" :key="item.id">{{item.name}}</li>
        <li class="search-item border-bottom" v-show="hasNoList">没有找到匹配数据</li>
      </ul>
    </div>
  </div>
</template>

<script>
import Bscroll from 'better-scroll'
import { mapMutations } from 'vuex'
export default {
  name: 'CitySearch',
  props: {
    cities: Object
  },
  data () {
    return {
      keyword: '',
      list: [],
      timer: null
    }
  },
  mounted () {
    this.scroll = new Bscroll(this.$refs.wrapper)
  },
  computed: {
    hasNoList () {
      return !this.list.length
    }
  },
  watch: {
    keyword () {
      if (this.timer) {
        clearTimeout(this.timer)
        this.timer = null
      }
      if (!this.keyword) {
        this.list = []
        return
      }
      this.timer = setTimeout(() => {
        const result = []
        for (let i in this.cities) {
          this.cities[i].forEach((value) => {
            if (value.spell.includes(this.keyword) || value.name.includes(this.keyword)) {
              result.push(value)
            }
          })
        }
        this.list = result
      }, 100)
    }
  },
  methods: {
    handleCityClick (city) {
      this.changeCity(city)
      this.$router.push('/')
    },
    ...mapMutations(['changeCity'])
  }
}
</script>

<style lang="stylus" scoped>
  @import '~@styles/varibles.styl'
  .search
    height .72rem
    padding 0 .1rem
    background $bgColor
    .search-input
      box-sizing border-box
      height .62rem
      line-height .62rem
      padding 0 .1rem
      width 100%
      text-align center
      border-radius .06rem
      color #666666
  .serach-content
    z-index 1
    overflow hidden
    position absolute
    top 1.58rem
    left 0
    right 0
    bottom 0
    background #eeeeee
    .search-item
      line-height .62rem
      padding-left .2rem
      background #ffffff
      color #666666
</style>

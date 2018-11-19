<template>
  <div class="wrapper">
    <swiper :options="swiperOption">
      <!-- slides -->
      <swiper-slide v-for="item of swiperlist" :key="item.id">
        <img class="swiper-img" :src="item.imgUrl" alt="">
      </swiper-slide>
      <!-- Optional controls -->
      <div class="swiper-pagination"  slot="pagination"></div>
    </swiper>
  </div>
</template>

<script>
export default {
  name: 'HomeSwiper',
  data () {
    return {
      swiperOption: {
        pagination: '.swiper-pagination',
        loop: true
      },
      swiperlist: [{
        id: '0001',
        imgUrl: 'http://img1.qunarzz.com/piao/fusion/1811/4d/6706bf772c05ce02.jpg_750x200_773e75f0.jpg'
      }, {
        id: '0002',
        imgUrl: 'http://img1.qunarzz.com/piao/fusion/1810/6e/4a5551bbb189d902.jpg_750x200_25257467.jpg'
      }]
    }
  }
}
</script>

<style lang='stylus' scoped>
  .wrapper >>> .swiper-pagination-bullet-active
    background: #ffffff
  .wrapper
    width: 100%
    height: 0
    overflow: hidden
    padding-bottom: 26.66667%
    background: #cccccc
    .swiper-img
      width: 100%

</style>

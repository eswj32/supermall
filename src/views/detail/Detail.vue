<template>
  <div id="detail">
    <detail-nav-bar class="detail-nav"></detail-nav-bar>
    <scroll class="content">
      <detail-swiper :top-images="topImages"></detail-swiper>
      <detail-base-info :goods="goods"></detail-base-info>
    </scroll>
    <detail-bottom-bar :addCart="addToCart"></detail-bottom-bar>
  </div>
</template>

<script>
import DetailNavBar from './childComps/DetailNavBar'
import DetailSwiper from './childComps/DetailSwiper'
import DetailBaseInfo from './childComps/DetailBaseInfo'
import DetailBottomBar from './childComps/DetailBottomBar'

import Scroll from 'components/common/scroll/Scroll'

import {getDetail, Goods, Shop} from 'network/detail'





export default {
  name:'Detail',
  data () {
    return {
      iid : null,
      topImages: [],
      goods: {},
      shop: {},
      detailInfo: []
    }
  },
  components: {
    DetailNavBar,
    DetailSwiper,
    DetailBaseInfo,
    DetailBottomBar,
    Scroll


  },
  methods: {
    addToCart() {
      const product = {}

      product.image = this.topImages[0];
      product.title = this.goodsInfo.title;
      product.desc = this.goodsInfo.desc;
      product.price = this.goodsInfo.realPrice;
      product.iid = this.iid;

      this.$store.dispatch('addCart', product)
    }
  },
  created() {

    this.iid = this.$route.params.iid

    getDetail(this.iid).then(res => {
      const data = res.result
      this.topImages = data.itemInfo.topImages
    })

    this.goods = new Goods(data.itemInfo, data.colums, data.shopInfo.services)

    this.shop = new Shop(data.shopInfo)

    this.detailInfo = data.detailInfo;
  }
}
</script>

<style  scoped>
#detail {
  position: relative;
  z-index: 9;
  background-color: #fff;
  height: 100vh;
}
.content {
  height: calc(100% - 44px - 49px);
}
.detail-nav {
  position: relative;
  z-index: 9;
  background-color: #fff;
}
</style>

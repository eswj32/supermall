<template>
  <div class="cart">
    <nav-bar>
      <div slot="center">购物车({{cartLength}})</div>
    </nav-bar>
    <cart-list></cart-list>
    <toast message="啊啊啊啊"></toast>
  </div>
</template>

<script>
import NavBar from 'components/common/navbar/NavBar'
import CartList from './childComps/CartList'
import Toast from 'components/common/toast/Toast'
import {mapGetters} from 'vuex'

export default {
  name:'Cart',
  data () {
    return {
    }
  },
  components: {
    NavBar,
    CartList,
    Toast
  },

    Toastcomputed: {
    // cartLength() {
    //   return this.$store.getters.cartLength
    // }
    ...mapGetters(['cartLength'])
  }
}
</script>

<style  scoped>
.cart {
  height: 100vh;
}
.nav-bar {
  background-color: var(--color-tint);
  color: #fff;
  font-weight: 700;
}
</style>

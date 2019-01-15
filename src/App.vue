<template>
  <div id="app">
    <Header :seller='seller' />
    <div class="tab">
        <router-link tag='div' to='/goods' class="tab-item">商品</router-link>
        <router-link tag='div' to='/ratings' class="tab-item">评论</router-link>
        <router-link tag='div' to='/seller' class="tab-item">商家</router-link>
    </div>
    <router-view></router-view>
  </div>
</template>

<script>
import Header from './components/header/Header'
export default {
  name: 'App',
  components: {
    Header
  },
  data () {
    return {
      seller: {},
      goods: {},
      ratings: {}
    }
  },
  mounted () {
    this.getData()
  },
  methods: {
    getData () {
      this.$http({
        method: 'get',
        url: '/api/data.json'
      }).then(this.getDataSucc)
    },
    getDataSucc (res) {
      const data = res.data
      this.seller = data.seller
      this.goods = data.goods
      this.ratings = data.ratings
    }
  }
}
</script>

<style lang="stylus" scoped>
  #app
    .tab
      display: flex
      width: 100%
      height: 40px
      line-height: 40px
      text-align: center
      .tab-item
        flex: 1
        font-size: 14px
        &.is-active
          color: rgb(240, 20, 20)
</style>

<template>
    <div class="header">
        <div class="content-wrapper">
            <div class="avatar">
                <img width='64' height='64' :src="seller.avatar" alt="">
            </div>
            <div class="content">
                <div class="title">
                    <span class="brand"></span>
                    <span class="name">{{seller.name}}</span>
                </div>
                <div class="description">
                    {{seller.description}}/{{seller.deliveryTime}}分钟送达
                </div>
                <div v-if="seller.supports" class="supports">
                    <span class="icon" :class='classMap[seller.supports[0].type]'></span>
                    <span class="text">{{seller.supports[0].description}}</span>
                </div>
            </div>
            <div
              v-if='seller.supports'
              class="support-count"
              @click='handleShowDetail'
            >
                <span class="count">{{seller.supports.length}}个</span>
                <i class="iconfont">&#xe604;</i>
            </div>
        </div>
        <div class="bulletin-wrapper">
            <span class="bulletin-title"></span><span class="bulletin-text">{{seller.bulletin}}</span>
            <i class="iconfont">&#xe604;</i>
        </div>
        <div class="background">
            <img :src="seller.avatar" alt="">
        </div>
        <div class="detail" v-if="showDetail" transition='fade'>
            <div class="detail-wrapper clearfix">
                <div class="detail-main">
                    <div class="name">{{seller.name}}</div>
                    <div class="star-wrapper">
                        <Star :size="48" :score="seller.score"></Star>
                    </div>
                    <div class="title">
                        <div class="line"></div>
                        <div class="text">优惠信息</div>
                        <div class="line"></div>
                    </div>
                    <ul v-if='seller.supports' class="supports">
                        <li
                          class="support-item"
                          v-for='(item, index) in seller.supports'
                          :key='index'
                        >
                            <span
                              class="icon"
                              :class='classMap[seller.supports[index].type]'
                            ></span>
                            <span class="text">{{seller.supports[index].description}}</span>
                        </li>
                    </ul>
                    <div class="title">
                        <div class="line"></div>
                        <div class="text">商家公告</div>
                        <div class="line"></div>
                    </div>
                    <div class="bulletin">
                        <p class="content">{{seller.bulletin}}</p>
                    </div>
                </div>
            </div>
            <div class="detail-close">
                <i class="iconfont" @click='handleShowDetail'>&#xe611;</i>
            </div>
        </div>
    </div>
</template>

<script>
import Star from '../star/Star'
export default {
  name: 'Header',
  props: {
    seller: {
      type: Object
    }
  },
  data () {
    return {
      showDetail: false
    }
  },
  created () {
    this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee']
  },
  methods: {
    handleShowDetail () {
      this.showDetail = !this.showDetail
    }
  },
  components: {
    Star
  }
}
</script>

<style lang="stylus" scoped>
@import '~styles/mixin.styl'
@import '~styles/base.styl'
  .header
    color: #fff
    position: relative
    overflow: hidden
    background: rgba(7, 17, 27, .5)
    .content-wrapper
      position: relative
      padding: 24px 12px 18px 24px
      font-size: 0
      .avatar
        display: inline-block
        vertical-align: top
        img
          border-radius: 2px
      .content
        display: inline-block
        margin-left: 16px
        .title
          margin: 2px 0 8px 0
          .brand
            display: inline-block
            vertical-align: top
            width: 30px
            height: 18px
            bg-image('brand')
            background-size: 30px 18px
            background-repeat: no-repeat
          .name
            font-size: 16px
            font-weight: bold
            line-height: 18px
            margin-left: 6px
        .description
          font-size: 12px
          font-weight: 200
          line-height: 12px
        .supports
          margin: 10px 0 2px 0
          .icon
            display: inline-block
            vertical-align: top
            width: 12px
            height: 12px
            margin-right: 4px
            background-size: 12px 12px
            background-repeat: no-repeat
            &.decrease
              bg-image('decrease_1')
            &.discount
              bg-image('discount_1')
            &.guarantee
              bg-image('guarantee_1')
            &.invoice
              bg-image('invoice_1')
            &.special
              bg-image('special_1')
          .text
            font-size: 10px
            font-weight: 200
            line-height: 12px
      .support-count
        position: absolute
        bottom: 18px
        right: 12px
        height: 10px
        font-size: 10px
        line-height: 12px
        padding: 7px 8px
        color: #fff
        font-weight: 200
        border-radius: 12px
        background: #333
        text-align: center
        .iconfont
          display: inline-block
          font-size: 6px
          margin-left: 2px
    .bulletin-wrapper
      position: relative
      height: 28px
      line-height: 28px
      padding: 0 22px 0 12px
      background: rgba(7, 17, 27, .2)
      white-space: nowrap
      overflow: hidden
      text-overflow: ellipsis
      .bulletin-title
        display: inline-block
        vertical-align: top
        margin-top: 8px
        width: 22px
        height: 12px
        bg-image('bulletin')
        background-size: 22px 12px
        background-repeat: no-repeat
      .bulletin-text
        font-size: 10px
        vertical-align: top
        font-weight: 200
        margin: 0 4px
      .iconfont
        position: absolute
        right: 5px
        bottom: 0
        font-size: 8px
    .background
      position: absolute
      top: 0
      left: 0
      right: 0
      width: 100%
      height: 100%
      filter: blur(10px)
      z-index: -1
      img
        width: 100%
        height: 100%
    .detail
      z-index: 9
      position: fixed
      top: 0
      left: 0
      width: 100%
      height: 100%
      overflow: auto
      background: rgba(7, 17, 27, .8)
      transition: all .5s
      &.fade-transition
        opacity: 1
      &.fade-enter,&.fade-leave
        opacity: 0
      .detail-wrapper
        min-height: 100%
        width: 100%
        .detail-main
          margin-top: 64px
          padding-bottom: 64px
          .name
            font-size: 16px
            font-weight: 700
            color: #fff
            line-height: 16px
            text-align: center
          .star-wrapper
            margin-top: 16px
            padding: 2px 0
            text-align: center
          .title
            display: flex
            margin: 28px 36px 24px 36px
            .line
              flex: 1
              position: relative
              top: -6px
              border-bottom: 1px solid rgba(255, 255, 255, .2)
            .text
              margin: 0 12px
              font-size: 14px
          .supports
            width: 80%
            margin: 0 auto
            font-size: 0
            .support-item
              padding: 0 12px
              margin-bottom: 12px
              &:last-child
                margin-bottom: 0
              .icon
                display: inline-block
                width: 16px
                height: 16px
                margin-right: 6px
                vertical-align: top
                background-size: 16px 16px
                background-repeat: no-repeat
                &.decrease
                  bg-image('decrease_2')
                &.discount
                  bg-image('discount_2')
                &.guarantee
                  bg-image('guarantee_2')
                &.invoice
                  bg-image('invoice_2')
                &.special
                  bg-image('special_2')
              .text
                font-size: 12px
                font-weight: 200
                color: #fff
                line-height: 12px
          .bulletin
            width: 80%
            margin: 0 auto
            .content
              margin: 0 12px
              font-size: 12px
              font-weight: 200
              color: #fff
              line-height: 24px
      .detail-close
        position: relative
        width: 32px
        height: 32px
        clear: both
        color: #fff
        margin: -64px auto 0 auto
        .iconfont
          font-size: 20px
</style>

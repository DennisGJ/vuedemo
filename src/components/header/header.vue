<template>
  <div class="header">
    <div class="content-wrapper">
      <div class="avatar">
        <img width="64" height="64" :src="seller.avatar" alt="">
      </div>
      <div class="content">
        <div class="title">
          <span class="brand"></span>
          <span class="name">{{seller.name}}</span>
        </div>
        <div class="description">
          {{seller.description}}/{{seller.deliveryTime}}分钟送达
        </div>
        <div v-if="seller.supports" class="support">
          <span class="icon" :class="classMap[seller.supports[0].type]"></span>
          <span class="text">{{seller.supports[0].description}}</span>
        </div>
      </div>
      <div v-if="seller.supports" class="support-count" @click="showDetail">
        <span class="count">{{seller.supports.length}}个</span>
        <i class="icon-keyboard_arrow_right"></i>
      </div>
    </div>
    <div class="bulletin-wrapper" @click="showDetail">
      <span class="bulletin-title"></span><span class="bulletin-text">{{seller.bulletin}}</span>
      <i class="icon-keyboard_arrow_right"></i>
    </div>
    <div class="background">
      <img :src="seller.avatar" alt="" width="100%" height="100%">
    </div>
    <div v-show="detailShow" class="detail">
      <div class="detail-wrapper clearfix">
        <div class="detail-main">

        </div>
      </div>
      <div class="detail-close" @click="hideDetail">
        <i class="icon-close"></i>
      </div>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
  export default {
    props: {
      seller: {
        type: Object
      }
    },
    data() {
      return {
        detailShow: false
      };
    },
    methods: {
      showDetail() {
        this.detailShow = true;
      },
      hideDetail() {
        this.detailShow = false;
      }
    },
    created() {
      this.classMap = ['decrease', 'discount', 'guarantee', 'invoice', 'special'];
    }
  };
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "../../common/stylus/mixin"

  .header
    position: relative
    color: #fff
    overflow: hidden
    background-color: rgba(7, 17, 27, 0.5)
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
        font-size: 0
        .title
          margin: 2px 0 8px 0
          .brand
            display: inline-block
            width: 30px
            height: 18px
            vertical-align: top
            bg-image('brand')
            background-size: 30px 18px
            background-repeat: no-repeat
          .name
            font-size: 16px
            margin-left: 6px
            color: rgb(255, 255, 255)
            font-weight: bold
            line-height: 18px
        .description
          font-size: 12px
          line-height: 12px
        .support
          margin-top: 10px
          .icon
            display: inline-block
            width: 12px
            height: 12px
            vertical-align: top
            margin-right: 4px
            background-size: 12px 12px
            background-repeat: no-repeat
            &.decrease
              bg-image(decrease_1)
            &.discount
              bg-image(discount_1)
            &.guarantee
              bg-image(guarantee_1)
            &.invoice
              bg-image(invoice_1)
            &.special
              bg-image(special_1)
          .text
            font-size: 10px
            line-height: 12px
      .support-count
        position: absolute
        right: 12px
        bottom: 18px
        height: 24px
        padding: 0 8px
        line-height: 24px
        border-radius: 14px
        background-color: rgba(0, 0, 0, 0.2)
        .count
          vertical-align: top
          font-size: 10px
        .icon-keyboard_arrow_right
          margin-left: 2px
          font-size: 10px
          line-height: 24px

    .bulletin-wrapper
      height: 28px
      line-height: 28px
      position: relative
      padding: 0 22px 0 12px
      white-space: nowrap
      overflow: hidden
      text-overflow: ellipsis
      background: rgba(7, 17, 27, 0.2)
      .bulletin-title
        display: inline-block
        width: 22px
        height: 12px
        bg-image(bulletin)
        background-size: 22px 12px
        background-repeat: no-repeat
      .bulletin-text
        font-size: 10px
        line-height: 28px
        margin: 0 4px
        vertical-align: top
      .icon-keyboard_arrow_right
        position: absolute
        right: 12px
        font-size: 10px
        top: 9px
    .background
      width: 100%
      height: 100%
      position: absolute
      left: 0
      top: 0
      z-index: -1
      filter: blur(10px)
    .detail
      position: fixed
      left: 0
      top: 0
      z-index: 100
      width: 100%
      height: 100%
      background: rgba(7, 17, 27, 0.8)
      .detail-wrapper
        min-height: 100%
        .detail-main
          margin-top: 64px
          padding-bottom: 64px
      .detail-close
        position: relative
        width: 32px
        height: 32px
        margin: -64px auto 0 auto
        clear: both
        font-size: 32px
</style>

<template>
  <div class="header">
  <div class="content-wapper">
   <div class="avatar">
      <img width="60" height="60" :src="seller.avatar" />   
   </div>
   <div class="content">
    <div class="title">
      <span class="brand"></span>
      <span class="name">{{seller.name}}</span>
    </div>
    <div class="discription">
      {{seller.description}}/{{seller.deliveryTime}}分钟送达
    </div>
    <div class="support" v-if="seller.supports">
      <span class="icon" :class="classMap[seller.supports[0].type]"></span>
      <span class="text">{{seller.supports[0].description}}</span>
    </div>
   </div> 
  </div>
  <div class="bullint-wapper">
    <span class="icon"></span>
    <span class="text">{{seller.bulletin}}</span>
  </div>
  <div class="background">
    <img :src="seller.avatar">
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
  created() {
    this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee'];
  }
};
</script>
<style lang="stylus" rel="stylesheet/stylus">
  @import "../../common/stylus/mixin.styl"

  .header
    color:#fff
    position:relative
    background:rgba(7,17,27,0.5)
    overflow: hidden
    .content-wapper
      padding:24px 12px 18px 24px
      font-size:0px
      .avatar
        display:inline-block
        font-size:14px
        img
          border-radius:5px
      .content
        display:inline-block
        font-size:14px
        margin-left:16px
        .title
          margin:2px 0 8px 0
          .brand
            width:30px
            height:18px
            vertical-align:top
            display:inline-block
            bg-image('brand')
            background-size:100% 100%
            background-repeat:no-repeat
          .name
            margin-left:6px
            font-size:16px
            line-height:18px
            color:rgb(255,255,255)
            font-weight:bold
        .discription
          margin-bottom:10px
          line-height:12px
          font-size:12px
        .support
          .icon
            display:inline-block
            width:12px
            height:12px
            margin-right:4px
            background-size:12px 12px
            background-repeat:no-repeat
            vertical-align:top
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
            font-size:12px
            line-height:12px
            vertical-align:top
    .bullint-wapper
      padding:10px 24px 0 12px
      height:28px
      overflow:hidden
      white-space:nowrap
      text-overflow: ellipsis
      background:rgba(7,17,27,.2)
      .icon
        bg-image('bulletin')
        width:24px
        height:16px
        display:inline-block
        background-size:100% 100%
        background-repeat:no-repeat
      .text
        vertical-align:top
    .background
      position:absolute
      top:0
      bottom:0
      right:0
      left:0
      z-index:-1
      filter:blur(10px)
      img
        width:100%
        height:100%
</style>
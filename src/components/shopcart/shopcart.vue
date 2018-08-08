<template>
    <div class="shopcart">
        <div class="content">
            <div class="content-left">
                <div class="logo-wrap">
                    <div class="logo">
                    </div>
                </div>
                <div class="price">
                    ￥0
                </div>
                <div class="desc">
                    另需配送费
                </div>
            </div>
            <div class="content-right">
                <div class="pay">$20起送</div>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    
}
</script>
<style scoped lang="stylus">
.shopcart
  position fixed
  left 0
  bottom 0
  height 48px
  width 100%
  background-color #141d27
  z-index 50
  .content
    display flex
    height 100%
    .content-left 
      flex 1
      .logo-wrap
        display inline-block
        width 58px
        height 58px
        margin 0 12px
        position relative
        top -10px
        vertical-align top
        background #141d27
        border-radius 50%
        .logo
          width 44px
          height 44px
          display inline-block
          margin 8px 0 8px 8px
          background-color #2b343c
          text-align center
          border-radius 50%
      .price
        display inline-block
        line-height 24px
        color rgba(255,255,255,0.3)    
        font-weight 700
        margin-top 12px
        padding-right 12px 
        border-right  1px solid rgba(255,255,255,0.1)  
      .desc
        display inline-block
        font-size 8px
        color rgba(255,255,255,0.4)
        font-weight 700
        line-height 24px
        padding-left 12px
    .content-right 
      flex 0 0 105px
      height 100%
      background-color #2b333b  
      display inline-block
      line-height 24px
      position relative
      .pay
        display inline-block
        color rgba(255,255,255,0.4)
        line-height 24px
        position absolute
        top 50%
        left 50%
        transform translateX(-50%) translateY(-50%)
        font-size 12px
</style>

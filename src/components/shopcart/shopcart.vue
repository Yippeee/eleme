<template>
    <div class="shopcart">
        <div class="content">
            <div class="content-left">
                <div class="logo-wrap">
                    <div class="logo">
                        <svg t="1533711596098" class="icon" style="" viewBox="0 0 1024 1024" version="1.1"
                            xmlns="http://www.w3.org/2000/svg" p-id="1039"
                            xmlns:xlink="http://www.w3.org/1999/xlink" width="30" height="30">
                            <path d="M246.4 912a2.1 2.1 0 1 0 134.4 0 2.1 2.1 0 1 0-134.4 0Z" p-id="1040" fill="#bfbfbf"></path>
                            <path d="M716.8 912a2.1 2.1 0 1 0 134.4 0 2.1 2.1 0 1 0-134.4 0Z" p-id="1041" fill="#bfbfbf"></path>
                            <path d="M905.6 764.8l-537.6 0c-28.8 0-57.6-25.6-64-54.4l-96-566.4c-9.6-54.4-60.8-96-115.2-96l-22.4 0c-12.8 0-25.6 12.8-25.6 25.6 0 12.8 12.8 25.6 25.6 25.6l22.4 0c28.8 0 57.6 25.6 64 54.4l96 566.4c9.6 54.4 60.8 96 115.2 96l537.6 0c12.8 0 25.6-12.8 25.6-25.6C931.2 777.6 921.6 764.8 905.6 764.8z" p-id="1042" fill="#bfbfbf"></path>
                            <path d="M880 179.2l-572.8 0c-12.8 0-25.6 12.8-25.6 25.6 0 12.8 12.8 25.6 25.6 25.6l572.8 0c25.6 0 38.4 16 32 41.6l-70.4 281.6c-6.4 32-41.6 57.6-73.6 60.8l-396.8 28.8c-12.8 0-25.6 12.8-22.4 28.8 0 12.8 12.8 25.6 28.8 22.4l396.8-28.8c54.4-3.2 105.6-48 118.4-99.2l70.4-281.6C976 230.4 937.6 179.2 880 179.2z" p-id="1043" fill="#bfbfbf"></path>
                        </svg>
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
          .icon 
            position: absolute;
            top: 16px;
            left: 14px;
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

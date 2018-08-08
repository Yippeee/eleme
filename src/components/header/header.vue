<template>
    <div class="header">
        <div class="content-wrapper">
            <div class="avatar">
                <img width="64" height="64" :src="seller.avatar">
            </div>
            <div class="content">
                <div class="title">
                    <span class="brand"></span>
                    <span class="name">{{seller.name}}</span>
                </div>
                <div class="description">
                    {{seller.description}}/{{seller.deliveryTime}}分钟送达
                </div>
                <div class="support" v-if="seller.supports">
                    <span class="icon"></span>
                    <span class="text">{{seller.supports[0].description}}</span>
                </div>
            </div>
            <div class="support-count" v-if="seller.supports" @click="showDetail">
              <span class="count">{{seller.supports.length}}个</span>
              <svg t="1533711315590" class="description_arrow" style="" viewBox="0 0 1024 1024" version="1.1"
                xmlns="http://www.w3.org/2000/svg" p-id="1150"
                xmlns:xlink="http://www.w3.org/1999/xlink" width="13" height="13">
                <path d="M312.888889 995.555556c-17.066667 0-28.444444-5.688889-39.822222-17.066667-22.755556-22.755556-17.066667-56.888889 5.688889-79.644445l364.088888-329.955555c11.377778-11.377778 17.066667-22.755556 17.066667-34.133333 0-11.377778-5.688889-22.755556-17.066667-34.133334L273.066667 187.733333c-22.755556-22.755556-28.444444-56.888889-5.688889-79.644444 22.755556-22.755556 56.888889-28.444444 79.644444-5.688889l364.088889 312.888889c34.133333 28.444444 56.888889 73.955556 56.888889 119.466667s-17.066667 85.333333-51.2 119.466666l-364.088889 329.955556c-11.377778 5.688889-28.444444 11.377778-39.822222 11.377778z" p-id="1151" fill="#ffffff"></path>
            </svg>
            </div>
        </div>
        <div class="bulletin-wrapper" @click="showDetail">
            <span class="board"></span>
            <span class="text">
              {{seller.bulletin}}
            </span>
        </div> 
        <div class="background">
            <img :src="seller.avatar" width="100%" height="100%">
        </div>
        <div class="detail" v-show="detailShow">
            <div class="detail-wrapper clearfix">
                <div class="detail-main">
                    <div class="main-header">
                        <span class="main-header-name">{{seller.name}}</span>
                        <star :num='seller.score'></star>
                    </div>
                    <div class="main-title">
                        <div class="line"></div>
                        <div class="main-title-text">优惠信息</div>
                        <div class="line"></div>
                    </div>
                    <ul class="supports">
                        <li class="supportsItem" v-for="supportsItem in seller.supports"><span :class="supportsItemMap[supportsItem.type]" class="supportsType"></span> <span class="supportsDes">{{supportsItem.description}}</span> </li>
                    </ul>
                    <div class="main-title">
                        <div class="line"></div>
                        <div class="main-title-text">商家公告</div>
                        <div class="line"></div>
                    </div>
                    <div>
                        <p class="main-bulletin">{{seller.bulletin}}</p>
                    </div>
                </div>
            </div>
            <div class="detail-close" @click="clodeDetail">X</div>
        </div>  
    </div>
</template>
<script>
/* eslint-disable */
import star from '../star/star'
export default {
    components:{star},
    props:{
      seller: {
        type: Object
      }
    },
    data() {
        return {
            avatar:'',
            name:'',
            detailShow:false,
            supportsItemMap : ['decrease','discount','guarantee','invoice','special']
        }
    },
    methods:{
        clodeDetail (){
            this.detailShow = false
        },
        showDetail (){
            this.detailShow = true
        }
    },
    watch:{
        seller:{
            handler (val){
                // console.log(JSON.stringify(val))
            },
            deep:true
        }
    }
}
</script>
<style lang="stylus" scoped>
.header
    position relative
    background-color  rgba(1,17,27,0.5)
    overflow hidden
    .content-wrapper
      padding 24px 12px 18px 24px
      font-size 0
      position relative
      .avatar
        display inline-block
        img 
          border-radius: 2px
      .content
        display inline-block
        vertical-align top
        margin-left  16px
        width 180px
        color rgb(255,255,255)
        .title
          display inline-block
          margin 2px 0 8px 0
          .brand
            display inline-block
            vertical-align top
            width 30px
            height 18px
            background-image url(../../../resource/img/brand@2x.png)
            background-repeat no-repeat
            background-size 30px 18px
            margin-right 6px
          .name
            font-size 16px
        .description
          display inline-block
          font-size 12px
          line-height 12px
        .support
          margin-top 10px
          .text
            font-size 10px
            line-height 12px  
            vertical-align top
          .icon
            background-image url(../../../resource/img/decrease_1@2x.png)
            background-size 12px 12px
            height 12px
            width 12px
            display inline-block
      .support-count
        position absolute
        right 12px
        bottom 18px
        padding 0px 8px
        background-color rgba(0,0,0,0.2)
        border-radius 14px
        height 24px
        line-height 28px
        text-align center
        color rgb(255,255,255)
        .count
          font-size 10px
          line-height 12px
        .description_arrow
          position relative  
          top 3px
          left 5px
        .icon-keyboard_arrow_right
          margin-left: 2px
          line-height: 24px
          font-size: 10px
    .bulletin-wrapper
      overflow hidden
      white-space nowrap
      text-overflow  ellipsis
      font-size 10px
      line-height 28px
      color rgb(255,255,255)
      vertical-align top
      position relative
      margin 0 12px
      .board
        background-image url(../../../resource/img/bulletin@2x.png)
        background-size 24px 12px
        display inline-block
        height 12px
        width 24px 
        position absolute
        top 8px
      .text
        vertical-align top   
        padding-left 28px
    .background
       display inline-block
       z-index -1
       position absolute
       left 0
       top 0
       width 100%
       height 100%
       filter: blur(10px)
    .detail
        position fixed 
        top 0px
        left 0px
        width 100%
        height 100%
        background-color rgba(7,17,27,0.8)   
        backdrop-filter: blur(10px)
        overflow auto
        z-index 100
        .detail-wrapper
            color rgb(255,255,255)
            min-height 100%
            width 100%
            .detail-main
              padding-bottom 32px
              margin-top 64px
              .main-header
                text-align center
                .main-header-name
                  font-weight 700
                  font-size 16px
              .main-title
                width 80%
                margin 12px auto
                .line
                  border-bottom 1px solid rgba(255,255,255,0.2)
                  top:-6px
                  display inline-block
                  width 37%
                  position relative
                .main-title-text
                  display inline-block 
                  font-weight 700
                  font-size 14px
              .main-bulletin
                margin 24px 48px 0 48px   
                font-size 12px
                font-weight 200px
                line-height 24px
                color white
              .supports
                margin-left 40px
                .supportsItem
                  .supportsType
                    display inline-block
                    width 16px
                    height 16px
                    vertical-align top
                    background-size 16px 16px 
                    background-repeat no-repeat
                    margin-bottom 10px
                    margin-right 10px
                    &.decrease
                      background-image url(../../../resource/img/decrease_1@2x.png)
                    &.discount
                      background-image url(../../../resource/img/discount_1@2x.png)  
                    &.guarantee
                      background-image url(../../../resource/img/guarantee_1@2x.png) 
                    &.invoice
                      background-image url(../../../resource/img/invoice_1@2x.png) 
                    &.special
                      background-image url(../../../resource/img/special_1@2x.png) 
        .detail-close
            color rgb(255,255,255)
            text-align center
            position relative
            width 100%
            clear both
            margin-top -32px
            height 32px
            font-size 32px
.clearfix
  display inline-block
.clearfix:after
  display block
  clear both
  content '.'
  visibility hidden
  line-height 0            
</style>

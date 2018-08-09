<template>
    <div class="shopcart">
        <div class="content">
            <div class="content-left clearfix" @click="showList">
                <div class="logo-wrap">
                    <div class="logo" :class="{'logo-acitve':total>0}">
                        <svg t="1533711596098" class="icon" style="" viewBox="0 0 1024 1024" version="1.1"
                            xmlns="http://www.w3.org/2000/svg" p-id="1039"
                            xmlns:xlink="http://www.w3.org/1999/xlink" width="30" height="30">
                            <path d="M246.4 912a2.1 2.1 0 1 0 134.4 0 2.1 2.1 0 1 0-134.4 0Z" p-id="1040" fill="#bfbfbf"></path>
                            <path d="M716.8 912a2.1 2.1 0 1 0 134.4 0 2.1 2.1 0 1 0-134.4 0Z" p-id="1041" fill="#bfbfbf"></path>
                            <path d="M905.6 764.8l-537.6 0c-28.8 0-57.6-25.6-64-54.4l-96-566.4c-9.6-54.4-60.8-96-115.2-96l-22.4 0c-12.8 0-25.6 12.8-25.6 25.6 0 12.8 12.8 25.6 25.6 25.6l22.4 0c28.8 0 57.6 25.6 64 54.4l96 566.4c9.6 54.4 60.8 96 115.2 96l537.6 0c12.8 0 25.6-12.8 25.6-25.6C931.2 777.6 921.6 764.8 905.6 764.8z" p-id="1042" fill="#bfbfbf"></path>
                            <path d="M880 179.2l-572.8 0c-12.8 0-25.6 12.8-25.6 25.6 0 12.8 12.8 25.6 25.6 25.6l572.8 0c25.6 0 38.4 16 32 41.6l-70.4 281.6c-6.4 32-41.6 57.6-73.6 60.8l-396.8 28.8c-12.8 0-25.6 12.8-22.4 28.8 0 12.8 12.8 25.6 28.8 22.4l396.8-28.8c54.4-3.2 105.6-48 118.4-99.2l70.4-281.6C976 230.4 937.6 179.2 880 179.2z" p-id="1043" fill="#bfbfbf"></path>
                        </svg>
                    </div>
                    <div class="number" v-show="num>0">{{num}}</div>
                </div>
                <div class="price" :class="{'price-acitve':total>0}">
                    ￥{{total}}
                </div>
                <div class="desc">
                    另需配送费￥{{deliver}}
                </div>
            </div>
            <div class="content-right clearfix" :class="{'enough':this.total>=this.minPrice}">
                <div class="pay" >{{completeString}}</div>
            </div>
        </div>
        <transition name='fade'>
            <div class="list clearfix" v-if="showMask" >
                <div class="list-header">
                    <span class="shopcar">购物车</span>
                    <span class="removeAll" @click.stop.prevent="removeAll">清空</span>
                </div>
                <div class="list-content" ref="list">
                    <ul>
                        <li class="food" v-for="food in selectfoods">
                            <span class="name">{{food.name}}</span>
                            <span class="price">￥{{food.price}}</span>
                            <cartcontrol :food='food'></cartcontrol>
                        </li>
                    </ul>
                </div>
            </div>
        </transition>  
        <div class="mask" v-show="showMask" @click="cancleMask()"></div>
    </div>
</template>
<script>
import cartcontrol from '../cartcontroler/cartcontroler'
import BScroll from "better-scroll"

export default {
    props:['selectfoods',"deliver","minPrice"],
    components:{
        cartcontrol
    },
    data() {
        return {
            showMask: false
        }
    },
    watch:{
        showMask() {
            console.log('chch')
            this.$nextTick(() => {
                new BScroll(this.$refs.list,{
                click: true
                })
            })
        }
    },
    computed:{
        total() {
            let i = 0
            this.selectfoods.forEach(food => {
                i += food.num*food.price
            });
            if(i == 0){
                this.showMask = false
            }
            return i
        },
        num(){
            let i = 0
            this.selectfoods.forEach(food => {
                i += food.num
            });
            return i
        },
        completeString() {
            if(this.total === 0){
                return `￥${this.minPrice}起送`
            }else if(this.total < this.minPrice-0){
                return `还差￥${this.minPrice-this.total}起送`
            }else{ 
                return '去结算'
            }
        }
    },
    methods:{
        showList (){
            if(this.total>0){
              this.showMask = !this.showMask
            }
        },
        removeAll (){
            this.selectfoods.forEach(item => {
                item.num = 0
            })
        },
        cancleMask() {
            this.showMask = false            
        }
        
    }
}
</script>
<style scoped lang="stylus">
@import "../../common/stylus/mixin.styl"
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
      z-index 50
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
        z-index 50
        .logo
          width 44px
          height 44px
          display inline-block
          margin 6px 0 0 6px
          background-color #2b343c
          text-align center
          border-radius 50%
          .icon 
            position: absolute;
            top: 16px;
            left: 14px;
        .number
          position absolute
          top 0px
          left 36px
          background-color rgb(240,20,20)
          width 24px
          line-height 16px
          font-size 9px
          font-weight 700
          border-radius 14px
          text-align center
          color rgb(255,255,255)    
        .logo-acitve
          background-color #00a0dc    
      .price
        display inline-block
        line-height 24px
        color rgba(255,255,255,0.3)    
        font-weight 700
        margin-top 12px
        padding-right 12px 
        border-right  1px solid rgba(255,255,255,0.1)
        z-index 50
      .price-acitve
        color rgba(255,255,255,1)    
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
      z-index 50
      .pay
        display inline-block
        width 100%
        color rgba(255,255,255,0.4)
        line-height 48px
        position absolute
        font-size 12px
        text-align center
      &.enough
        background #00b43c
        .pay
          color rgba(255,255,255,1)
          text-align center
  .list
    position absolute
    width 100%
    bottom 48px
    left 0px
    z-index -1
    transform translate3d(0,0,0)
    .list-header
      height 40px
      background-color #f3f5f7
      .shopcar
        margin-left 18px
        font-size 14px
        font-weight 200
        color rgb(7,17,27)
        line-height 40px
      .removeAll
        position absolute
        right 18px
        font-size 12px
        line-height 40px
        color rgb(0,160,220)  
    .list-content
      max-height 217px  
      background white
      padding 0 18px
      overflow hidden
      .food
        height 48px
        border-1px(rgba(7,17,27,0.1))
        .name
          font-size 14px
          line-height 48px
          color rgb(7,17,27)
        .price
          position absolute
          font-size 14px
          line-height 48px
          color rgb(7,17,27)
          right 80px
        .cartcontroler-wrap
          bottom: 0px;
          right: 0px;
          top: 7px;
    &.fade-enter,&.fade-leave-to
      transform translate3d(0,100%,0)
    &.fade-enter-active,&.fade-leave-active
      transition all .2s ease
    &.fade-enter-to,&.fade-leave
      transform translate3d(0,0,0)        
  .mask
    position fixed
    z-index -2
    top 0px
    left 0px
    width 100%
    height 100%
    background rgba(7,17,27,0.6)          
</style>

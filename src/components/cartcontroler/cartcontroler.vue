<template>
    <div class="cartcontroler-wrap">
        <transition name="move">
            <span v-show="food.num || food.num>0" @click="decrease($event)" class="span-decrease clearfix">
                <svg t="1533714167213" class="icon-decrease"  viewBox="0 0 1024 1024" version="1.1"
                    xmlns="http://www.w3.org/2000/svg" p-id="5835"
                    xmlns:xlink="http://www.w3.org/1999/xlink" width="24" height="24">
                    <path d="M696 480H328c-4.4 0-8 3.6-8 8v48c0 4.4 3.6 8 8 8h368c4.4 0 8-3.6 8-8v-48c0-4.4-3.6-8-8-8z" p-id="5836" fill="#1296db"></path>
                    <path d="M512 64C264.6 64 64 264.6 64 512s200.6 448 448 448 448-200.6 448-448S759.4 64 512 64z m0 820c-205.4 0-372-166.6-372-372s166.6-372 372-372 372 166.6 372 372-166.6 372-372 372z" p-id="5837" fill="#1296db"></path>
                </svg>
            </span>
        </transition>
        <transition >
            <div class="num" v-show="food.num || food.num>0">{{this.food.num}}</div>
        </transition>
        <span @click="add($event)" class="clearfix">
            <svg t="1533713251355" class="icon-add" style="" viewBox="0 0 1024 1024" version="1.1"
            xmlns="http://www.w3.org/2000/svg" p-id="6086"
            xmlns:xlink="http://www.w3.org/1999/xlink" width="24" height="24">
            <path d="M512 64C264.6 64 64 264.6 64 512s200.6 448 448 448 448-200.6 448-448S759.4 64 512 64z m192 472c0 4.4-3.6 8-8 8H544v152c0 4.4-3.6 8-8 8h-48c-4.4 0-8-3.6-8-8V544H328c-4.4 0-8-3.6-8-8v-48c0-4.4 3.6-8 8-8h152V328c0-4.4 3.6-8 8-8h48c4.4 0 8 3.6 8 8v152h152c4.4 0 8 3.6 8 8v48z" p-id="6087" fill="#1296db"></path>
            </svg>
        </span>
    </div>
</template>
<script>
import Vue from 'vue';
export default {
    props:['food'],
    data (){
        return {
        }
    },
    methods:{
        add(event) {
            if (!event._constructed) {
               return;
            }
            if(!this.food.num){
                Vue.set(this.food,'num',1)
                console.log(this.food.num)
            }else{
                this.food.num++
            }
        },
        decrease(event) {
            if (!event._constructed) {
               return;
            }
            if(this.food.num > 0){
               this.food.num--
            }
        }
    }
}
</script>
<style lang="stylus" scoped>
.cartcontroler-wrap
  position absolute
  right 18px
  bottom 18px
  font-size 0
  height 34px
  .span-decrease
    transform translate3d(0.0.0)
    .icon-decrease
      padding 5px
    //进入的开始和离开的结束
    &.move-enter,&.move-leave-to
      opacity 0
      transform translate3d(24px,0,0)
      .icon-decrease
        transform rotate(180deg)
    //整个过程的中间状态
    &.move-enter-active,&.move-leave-active
      transition all .5s linear 
      .icon-decrease
        transition all .5s linear
    //进入的结束和离开时候的开始
    &.move-enter-to,&.move-leave
      opacity 1
      transform translate3d(0,0,0)
      .icon-decrease
        transform rotate(0deg)
.num
  display inline-block
  font-size 10px
  line-height 24px
  position relative
  top -14px
.icon-add
  padding  5px
</style>



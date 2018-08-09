<template>
  <div id="app">
    <v-header :seller='seller'></v-header>
    <div class="hav border-1px">
      <div class="havItem">
        <router-link to="/goods">{{havArr[0]}}</router-link>
      </div>
      <div class="havItem">
        <router-link to="/rating">{{havArr[1]}}</router-link>
      </div>
      <div class="havItem">
        <router-link to="/seller">{{havArr[2]}}</router-link>
      </div>
    </div>
    <keep-alive>
      <router-view :seller="seller"></router-view>
    </keep-alive>
  </div>
</template>

<script>
/* eslint-disable */
import header from '@/components/header/header'

export default {
  components :{ 'v-header': header},
  data() {
    return {
      havArr:['商品','评论','商家'],
      seller:{}
    };
  },
  created (){
    this.$http.get('/api/seller').then((res) =>{
      this.seller = res.body.data
    })
  }
}
</script>

<style lang='stylus' scoped>
@import "./common/stylus/index.styl"

#app 
  font-family: 'Avenir', Helvetica, Arial, sans-serif
  -webkit-font-smoothing: antialiased
  -moz-osx-font-smoothing: grayscale
  color: #2c3e50
  .hav
    display flex
    width 100%
    height 40px
    line-height 40px
    justify-content center
    border-1px(rgba(1,17,27,0.1))
    .havItem
      text-align: center
      // flex 1 1 auto =
      flex 1
      & > a
        display block
        font-size 14px
        color rgb(77, 85, 93)
        &.router-link-active
          color rgb(240, 20, 20)
</style>

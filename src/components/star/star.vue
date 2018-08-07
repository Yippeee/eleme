<template>
    <div>
        <div v-for="(starClass,index) in starClasses" class="item" :class="starClass"></div>
    </div>
</template>
<script>
export default {
    /* eslint-disable */
    props:['num'],
    created (){
        console.log('num: '+this.num)
    },
    methods:{
        checkNum (n){
            let a = 0;
            for(;n>0;n--){
                a++
            }
        }
    },
    computed:{
        starClasses (){
            let result = [],
                number = this.num,
                remainder = number%1;
            for(;number>=1;number--){
                result.push('on')
            }
            if(remainder !== 0){
                if(remainder > 0.5){
                    result.push('half')
                }else{
                    result.push('off')
                }
                number--
            }
            for(;number>=1;number--){
                result.push('off')
            }
            console.log(result)
            return result;
        }
    }
}
</script>
<style lang='stylus' scoped>
    .item
      font-size 20px
      width 20px
      height 20px
      margin 20px auto
      display inline-block
      margin-right 20px
      &.on
        background-image url(../../../resource/img/star24_on@2x.png)
      &.half
        background-image url(../../../resource/img/star24_half@2x.png)
      &.off
        background-image url(../../../resource/img/star24_off@2x.png)       
</style>

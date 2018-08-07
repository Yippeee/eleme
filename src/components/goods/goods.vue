<template>
    <div class="goods">
        <div class="manu-wrap">
            <ul>
                <li class="manu-list border-1px" v-for="item in goods">
                    <span class="text">
                       {{item.name}}
                    </span>
                </li>
            </ul>
        </div>
        <div class="food-wrap">
            <ul>
                <li v-for="item in goods"> 
                    <h1 class="title">{{item.name}}</h1>
                    <ul>
                        <li class="good-items border-1px" v-for="good in item.foods">
                            <div class="icon">
                                <img :src="good.icon">
                            </div>
                            <div class="content">
                                <h2 class="name">{{good.name}}</h2>
                                <p class="desc">{{good.description}}</p>
                                <div class="extra">
                                    <span class="count">月售{{good.sellCount}}份</span>
                                    <span>好评率{{good.rating}}%</span>
                                </div>
                                <div class="price">
                                    <span class="now">￥{{good.price}}</span>
                                    <span class="old" v-show="good.oldPrice">￥{{good.oldPrice}}</span>
                                </div>
                            </div>
                        </li>
                    </ul>
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
/* eslint-disable */
export default {
  data() {
    return {
      goods: {}
    };
  },
  created() {
    this.$http.get("/api/goods").then(res => {
      this.goods = res.body.data;
      console.log(this.goods);
    });
  }
};
</script>

<style lang="stylus" scoped>
@import '../../common/stylus/index.styl';

.goods {
    position: absolute;
    width: 100%;
    top: 174px;
    bottom: 46px;
    display: flex;
    overflow: hidden;

    .manu-wrap {
        flex: 0 0 80px;
        background-color: #f3f5f7;
        width: 80px;

        .manu-list {
            height: 54px;
            padding: 0 12px;
            display: table;
            border-1px(rgba(1, 17, 27, 0.1));

            .text {
                display: table-cell;
                font-size: 12px;
                font-weight: 200;
                line-height: 14px;
                color: rgb(7, 17, 27);
                vertical-align: middle;
            }
        }
    }

    .food-wrap {
        flex: 1;

        .title {
            padding-left: 14px;
            border-left: 2px solid #d9dde1;
            height: 26px;
            font-size: 12px;
            line-height: 26px;
            color: rgb(147, 153, 159);
            background-color: #f3f5f7;
        }

        .good-items {
            padding 18px
            display flex
            border-1px(rgba(1, 17, 27, 0.1));
            .icon {
                flex 0 0 57px
                width 57px
                img {
                    width: 57px;
                    height: 57px;
                }
            }
            .content{
                flex 1
                margin-left 5px
                .name{
                    margin-top 2px
                    font-size 14px
                    color rgb(7,17,27)
                    line-height 14px
                }
                .desc,.extra{
                    font-size 10px
                    color rgb(147,153,159)
                    margin 8px 0 0 0
                }
                .price{
                    .now{
                        color red
                        font 10px
                        line-height 24px
                        font-weight 700
                    }
                    .old{
                        font-size 10px
                        color rgb(147,153,159)
                        font-weight 700
                        text-decoration line-through
                    }
                }
            }
        }
    }
}
</style>


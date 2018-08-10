<template>
    <div class="goods">
        <div class="manu-wrap" ref="manuWrap">
            <ul>
                <li class="manu-list border-1px"  v-for="(item,index) in goods" :class="{'curr': index === currIndex}" @click="changeIndex(index,$event)">
                    <span class="text">
                       {{item.name}}
                    </span>
                </li>
            </ul>
        </div>
        <div class="food-wrap" ref="foodWrap">
            <ul>
                <li v-for="item in goods" class="good-item-hook"> 
                    <h1 class="title">{{item.name}}</h1>
                    <ul>
                        <li class="good-items border-1px " v-for="good in item.foods" @click="showfood(good)">
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
                            <cartcontroler :food="good"></cartcontroler>
                        </li>
                    </ul>
                </li>
            </ul>
        </div>
            <div class="food-wrap" >
                <div class="food-header">
                <div class="hearder-avatar">
                    <img :src="selectfood.image">
                </div>
                <div class="hearder-content">
                    <div class="content-name">{{selectfood.name}}</div>
                    <div class="extra">
                        <span class="mouth">月售{{selectfood.sellCount}}份</span>
                        <span class="rating">好评率{{selectfood.rating}}%</span>
                    </div>
                    <div class="price">
                        <span class="nowPrice">￥{{selectfood.price}}</span>
                        <span class="oldPrice">￥{{selectfood.oldPrice}}</span>
                    </div>
                </div>
            </div>
            <div class="food-intro"></div>
            <div class="food-rating">
                <div class="rating-header">
                    <div class="name">商品评价</div>
                    <div class="button-wrap border-1px">
                        <div class="button button-all">全部</div>
                        <div class="button button-recom">推荐</div>
                        <div class="button button-down">吐槽</div>
                    </div>
                    <svg t="1533866378468" class="icon" style="" viewBox="0 0 1024 1024" version="1.1"
                        xmlns="http://www.w3.org/2000/svg" p-id="1873"
                        xmlns:xlink="http://www.w3.org/1999/xlink" width="24" height="24">
                        <path d="M512 65.983389c-245.919634 0-446.016611 200.095256-446.016611 446.016611 0 245.952318 200.064292 446.016611 446.016611 446.016611S958.016611 757.952318 958.016611 512C958.016611 266.080366 757.952318 65.983389 512 65.983389zM727.231286 438.432254 471.00766 697.439161c-0.063647 0.063647-0.192662 0.096331-0.25631 0.192662-0.096331 0.063647-0.096331 0.192662-0.192662 0.25631-2.048757 1.983389-4.575729 3.19957-6.944443 4.544765-1.183497 0.672598-2.143368 1.696116-3.392232 2.176052-3.839484 1.536138-7.904314 2.33603-11.967424 2.33603-4.095794 0-8.224271-0.799892-12.096439-2.399677-1.279828-0.543583-2.303346-1.632469-3.519527-2.303346-2.368714-1.343475-4.832039-2.528692-6.880796-4.544765-0.063647-0.063647-0.096331-0.192662-0.159978-0.25631-0.063647-0.096331-0.192662-0.096331-0.25631-0.192662l-126.016611-129.503454c-12.320065-12.672705-12.032791-32.928047 0.639914-45.248112 12.672705-12.287381 32.895364-12.063755 45.248112 0.639914l103.26354 106.112189 233.279613-235.839269c12.416396-12.576374 32.704421-12.703669 45.248112-0.25631C739.520387 405.600538 739.647682 425.85588 727.231286 438.432254z" p-id="1874" fill="#bfbfbf"></path>
                    </svg>
                    <span>只看有内容的评价</span>
                </div>
                <div class="rating-content">
                    <ul>
                        <li v-for="item in selectfood.ratings">
                            {{item.username}}
                        </li>
                    </ul>
                </div>
            </div>
            </div>
            
        </div>
        <shopcart :selectfoods="selectfoods" :deliver="seller.deliveryPrice" :minPrice="seller.minPrice"></shopcart>
    </div>
</template>

<script>
/* eslint-disable */
import BScroll from "better-scroll";
import shopcart from "../shopcart/shopcart";
import cartcontroler from "../cartcontroler/cartcontroler";
export default {
  components: {
    shopcart,
    cartcontroler
  },
  props: ["seller"],
  data() {
    return {
      goods: {},
      heightArray: [],
      scrollY: 0,
      showFood: false,
      selectfood: {}
    };
  },
  computed: {
    currIndex() {
      for (let i = 0; i < this.heightArray.length; i++) {
        let height1 = this.heightArray[i];
        let height2 = this.heightArray[i + 1];
        let y = this.scrollY;
        if (y >= height1 - 5 && y < height2 - 5) {
          return i;
        }
      }
      return 0;
    },
    selectfoods() {
      let res = [];
      if (this.goods.length > 0) {
        this.goods.forEach(item => {
          item.foods.forEach(food => {
            if (food.num) {
              res.push(food);
            }
          });
        });
      }
      return res;
    }
  },
  created() {
    this.$http.get("/api/goods").then(res => {
      this.goods = res.body.data;
      this.$nextTick(() => {
        this._initScroll();
        this.heightArray.push(0);
        let height = 0;
        let dom = document.getElementsByClassName("good-item-hook");
        for (let i = 0; i < dom.length; i++) {
          height += dom[i].clientHeight;
          this.heightArray.push(height);
        }
      });
    });
  },
  methods: {
    _initScroll() {
      this.menuScroll = new BScroll(this.$refs.manuWrap, {
        click: true
      });
      this.foodScroll = new BScroll(this.$refs.foodWrap, {
        click: true,
        probeType: 3
      });
      this.foodScroll.on("scroll", pos => {
        this.scrollY = Math.abs(Math.round(pos.y));
      });
    },
    changeIndex(index, e) {
      if (!e._constructed) {
        return;
      }
      let el = document.getElementsByClassName("good-item-hook")[index];
      this.foodScroll.scrollToElement(el, 300);
    },
    showfood(good) {
      this.selectfood = good;
      console.log("ffffffffffffffffffffff");
      this.showFood = true;
      this.$nextTick(() => {
          new BScroll(this.$refs.food,{})
      })
    }
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
            width: 56px;
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

        .curr {
            color: rgb(240, 20, 20);
            background-color: white;
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
            padding: 18px;
            display: flex;
            position: relative;
            border-1px(rgba(1, 17, 27, 0.1));

            .icon {
                flex: 0 0 57px;
                width: 57px;

                img {
                    width: 57px;
                    height: 57px;
                }
            }

            .content {
                flex: 1;
                margin-left: 5px;

                .name {
                    margin-top: 2px;
                    font-size: 14px;
                    color: rgb(7, 17, 27);
                    line-height: 14px;
                }

                .desc, .extra {
                    font-size: 10px;
                    color: rgb(147, 153, 159);
                    margin: 8px 0 0 0;
                }

                .price {
                    .now {
                        color: red;
                        font: 10px;
                        line-height: 24px;
                        font-weight: 700;
                    }

                    .old {
                        font-size: 10px;
                        color: rgb(147, 153, 159);
                        font-weight: 700;
                        text-decoration: line-through;
                    }
                }
            }
        }
    }

    .food {
        position: fixed;
        top: 0px;
        left: 0px;
        width: 100%;
        height: 100%;
        background-color: #fff;

        .food-header {
            .hearder-avatar{
                img {
                    width: 100%;
                    heigh: 100%;
                }
            }
            .hearder-content{
                padding 18px
                border-bottom 16px solid #f3f5f7
                .content-name{
                    margin-bottom 8px
                    font-size 14px
                    font-weight 700
                    color rgb(7,17,27)
                    line-height 14px
                }
                .extra{
                    font-size 10px
                    line-height 10px
                    color rgb(147,153,159)
                }
                .price{
                    margin-top 18px
                    .nowPrice{
                        font-size 14px
                        font-weight 700
                        color rgb(240,20,20) 
                        line-height 24px
                    }
                    .oldPrice{
                        font-size 10px
                        font-weight 700
                        color rgb(147,153,159)
                        line-height 24px
                        text-decoration line-through
                    }
                }
            }
            
        }
        .food-rating{
            .rating-header{
              padding 18px 18px 12px 18px
              .name{
                  color rgb(7,17,27)
                  font-size 14px
                  line-height 14px
              }
              .button-wrap{
                  margin 18px 0
                  border-1px(rbga(7,17,27,0.1))
                  .button{
                      display inline-block
                      padding 8px 12px
                      font-size 12px
                      line-height 16px
                      margin-right 8px
                      text-align center
                      border-radius 2px
                  }
                  .button-all{
                      background-color rgb(0,160,220)
                      color rgb(255,255,255)
                  }
                  .button-recom{
                    background-color rgba(0,160,220,0.2)
                    color rgb(77,85,93)
                  }
                  .button-down{
                    color rgb(77,85,93)
                    background-color rgba(77,85,93,0.2)
                  }
              }
            }
        }
    }
}
</style>


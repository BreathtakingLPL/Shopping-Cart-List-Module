<template>
  <div class="goods-container">
    <!-- 左侧图片 left img-->
    <div class="thumb">
      <div class="custom-control custom-checkbox">
        <!-- 复选框 check box-->
        <input type="checkbox" class="custom-control-input" :id='"cb" +id' :checked="state" @change='getState'/>
        <label class="custom-control-label" :for= '"cb" +id'>
          <!-- 商品的缩略图 goods pic-->
          <img :src="pic" alt="" />
        </label>
      </div>
    </div>
    <!-- 右侧信息区域 Right info section-->
    <div class="goods-info">
      <!-- 商品标题 Goods title-->
      <h6 class="goods-title">{{title}}</h6>
      <div class="goods-info-bottom">
        <!-- 商品价格 goods price-->
        <span class="goods-price">￥{{price}}</span>
        <!-- 商品的数量 goods amount-->
        <Counter :num='count' :id='id'></Counter>
      </div>
    </div>
  </div>
</template>

<script>
// import Couter component 
// import Counter from '@/components/Counter/Ccounter.vue'
import Counter from '../Counter/Counter.vue'
export default {
  props: {
    id: {
      type: Number,
      required: true
    },
    // goods title
    title: {
      type: String,
      default: ''
    },
    // goods image
    pic: {
      type: String,
      default: ''
    },
    // goods price
    price: {
      default: 0,
      type: Number
    },
    // goods state
    state: {
      type: Boolean,
      default: true
    },
    // goods amount
    count: {
      type: Number,
      default:1
    }
  },
  methods: {
    getState(e) {
      const stateObj = {id:this.id, newState:e.target.checked}
      this.$emit('stateChange',stateObj)
    }
  },
  components: {
    Counter
  }
}
</script>

<style lang="less" scoped>
.goods-container {
  + .goods-container {
    border-top: 1px solid #efefef;
  }
  padding: 10px;
  display: flex;
  .thumb {
    display: flex;
    align-items: center;
    img {
      width: 100px;
      height: 100px;
      margin: 0 10px;
    }
  }

  .goods-info {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    flex: 1;
    .goods-title {
      font-weight: bold;
      font-size: 12px;
    }
    .goods-info-bottom {
      display: flex;
      justify-content: space-between;
      .goods-price {
        font-weight: bold;
        color: red;
        font-size: 13px;
      }
    }
  }
}
</style>

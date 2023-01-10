<template>
  <div class="number-container d-flex justify-content-center align-items-center">
    <!-- 减 1 的按钮 subtract 1 button-->
    <button type="button" class="btn btn-light btn-sm" @click='sub'>-</button>
    <!-- 购买的数量 amouont of goods-->
    <span class="number-box">{{num}}</span>
    <!-- 加 1 的按钮  plus 1 button-->
    <button type="button" class="btn btn-light btn-sm" @click='add'>+</button>
  </div>
</template>

<script>
// import bus
import bus from '@/components/eventBus.js'

export default {
  methods: {
    add() {
      const countObj = {id:this.id, value: this.num + 1}
      bus.$emit('share', countObj)
    },
    sub() {
      if (this.num -1 === 0) return
      const countObj = {id:this.id, value: this.num - 1}
      bus.$emit('share', countObj)
    }
  },
  props: {
    // reveive specific goods id
    id: {
      type: Number,
      required:true
    },
    // receive amount from Goods
    num: {
      type: Number,
      default:1
    }
  }
}
</script>

<style lang="less" scoped>
.number-box {
  min-width: 30px;
  text-align: center;
  margin: 0 5px;
  font-size: 12px;
}

.btn-sm {
  width: 30px;
}
</style>

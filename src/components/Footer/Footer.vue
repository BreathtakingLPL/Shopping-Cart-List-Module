<template>
  <div class="footer-container">
    <!-- 左侧的全选 Left select all checkbox-->
    <div class="custom-control custom-checkbox">
      <input type="checkbox" class="custom-control-input" id="cbFull" :checked="fullState" @change='fullChange'/>
      <label class="custom-control-label" for="cbFull">Select All</label>
    </div>

    <!-- 中间的合计 total price in the middle-->
    <div>
      <span>Total：</span>
      <span class="total-price">￥{{ totalAmt.toFixed(2) }}</span>
    </div>

    <!-- 结算按钮 Checkout-->
    <button type="button" class="btn btn-primary btn-settle">Checkout({{ allCount }})</button>
  </div>
</template>

<script>
export default {
  methods: {
    fullChange(e) {
      this.$emit('full-change', e.target.checked)
    }
  },
  props: {
    fullState: {
      type: Boolean,
      default: false
    },
    totalAmt: {
      type: Number,
      default:0
    },
    allCount: {
      type: Number,
      default:0
    }
  }
}
</script>

<style lang="less" scoped>
.footer-container {
  font-size: 12px;
  height: 50px;
  width: 100%;
  border-top: 1px solid #efefef;
  position: fixed;
  bottom: 0;
  background-color: #fff;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 10px;
}

.custom-checkbox {
  display: flex;
  align-items: center;
}

#cbFull {
  margin-right: 5px;
}

.btn-settle {
  height: 80%;
  min-width: 110px;
  border-radius: 25px;
  font-size: 12px;
}

.total-price {
  font-weight: bold;
  font-size: 14px;
  color: red;
}
</style>

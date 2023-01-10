<template>
  <div class="app-container">
    <h1>Order list</h1>
    <Header></Header>
    <Goods v-for="item in list" :key="item.id" :title="item.goods_name" :id='item.id' :count='item.goods_count' :pic='item.goods_img' :price='item.goods_price' :state='item.goods_state' @stateChange='getNewState'></Goods>
    <Footer :fullState='fullState' :totalAmt= 'amt' :allCount='totalAmount' @full-change='getFullState'></Footer>
  </div>
</template>

<script>

// 导入header组件， import Header component
import Header from '@/components/Header/Header.vue'

// 导入Goods组件， import Goods component
import Goods from '@/components/Goods/Goods.vue'

// 导入Footer组件， import Footer component
import Footer from '@/components/Footer/Footer.vue'

// 导入axios, import axios
import axios from 'axios'

// import bus
import bus from '@/components/eventBus.js'


export default {
  data () {
    return {
      list: [] //cart data list
    }
    
  },
  computed: {
    fullState() {
      return this.list.every(item => item.goods_state)
    },
    //  calculate all the goods price
    amt() {

      return this.list.filter(item => item.goods_state).reduce((total,item) => {
        return total += item.goods_price * item.goods_count
      },0)
    },
    // calculate all the selected goods amount
    totalAmount() {
      return this.list.filter(item => item.goods_state).reduce((total, item) => {
        return total += item.goods_count 
      },0)
    }
  },
  methods: {
    async initCartList () {
      const { data:res } = await axios.get('https://www.escook.cn/api/cart')
      console.log(res)
      if (res.status === 200) {
        this.list = res.list
      }
    },
    //update new state from Goods
    getNewState (e) {
      this.list.some(item => {
        if(item.id === e.id) {
          item.goods_state= e.newState
          return true
        }  
      })
    },
    // receive full state from Footer
    getFullState(val) {
      this.list.forEach(item => item.goods_state = val)
    }
  },
  created () {
    this.initCartList()
    // receive amout from Couter via bus
    bus.$on('share', val => {
      this.list.some(item => {
        if (item.id === val.id) {
          item.goods_count = val.value
        }
      })
    })
  },
  components: {
    Header,
    Goods,
    Footer
  }
}
</script>

<style lang="less" scoped>
.app-container {
  padding-top: 45px;
  padding-bottom: 50px;
}
</style>

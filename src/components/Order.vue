<template>
  <div class="content">
    <el-table
      class="el-table"
      ref="multipleTable"
      :data="order"
      tooltip-effect="dark"
      style="width: 100%"
    >
      <el-table-column type="selection" width="25"></el-table-column>
      <el-table-column label="商品" width="440">
        <template slot-scope="scope">
          <img class="thumbnail-goods" :src="scope.row.cover" />
          &nbsp;
          {{ scope.row.text }}
        </template>
      </el-table-column>
      <el-table-column prop="price" label="单价" width="160"></el-table-column>
      <el-table-column prop="quantity" label="数量" show-overflow-tooltip>
     <template slot-scope="scope">
        {{scope.row.quantity }}
       </template> 
      </el-table-column>
      <el-table-column prop="sum" label="金额" width="160">
        <template slot-scope="scope">￥{{ scope.row.price * scope.row.quantity }}</template>
      </el-table-column>
      <el-table-column label="操作" width="200">
        <template slot-scope="scope">
          <el-button class="btn-text" @click="drop(scope.$index)" type="text" size="small">退款</el-button>
        </template>
      </el-table-column>
    </el-table>
    <table class="table-goods" v-if="order.length">
       <el-button class="el-row-button" @click="payAll">结算</el-button>
    </table>
  
    <div class="placeholder" v-else>当前并无订单！快去下单吧~~</div>
  </div>
</template>

<script>
  export default {
    name: 'Cart',
    data () {
      return {
        order: [],
        cart: []
      }
    },
    mounted () {
      this.$nextTick(function () {
        this.getStore()
      })
    },
    methods: {
      getStore () {
        let gsStore = window.localStorage.getItem('gsStore')
        if (gsStore) {
          gsStore = JSON.parse(gsStore)
          this.cart = gsStore.cart || []
          this.order = gsStore.order || []
        }
      },
      setStore () {
        let gsStore = {
          cart: this.cart,
          order: this.order
        }
        window.localStorage.setItem('gsStore', JSON.stringify(gsStore))
      },
      drop (index) {
        this.order.splice(index, 1)
        this.setStore()
      }
    }
  }
</script>

<style scoped>
.el-row-button{
  background-color:rgb(12, 145, 12);
  color: #fff;
  width: 120px;
  float: right;}
  .content {
    width: 1120px;
    margin-left: auto;
    margin-right: auto;
  }
  .one-line {
    word-break: break-all;
    white-space: nowrap;
    text-overflow: ellipsis;
    overflow: hidden;
  }
  .table-goods {
    width: 100%;
    margin-top: 15px;
    color: #555;
    table-layout: fixed;
    border-collapse: collapse;
    user-select: none;
    cursor: default;
  }
  .table-goods>tbody>tr {
    transition: background-color 200ms linear;
    border-top: 1px solid #ebeef5;
  }
  .table-goods>tbody>tr:last-child {
    border-bottom: 1px solid #ebeef5;
  }
  .table-goods>tbody>tr:hover {
    background-color: rgba(149, 191, 103, .1);
  }
  .table-goods th,
  .table-goods td {
    text-align: left;
    font-size: 16px;
    padding-left: 12px;
  }
  .table-goods th {
    line-height: 52px;
  }
  .table-goods td {
    line-height: 120px;
  }
  .thumbnail-goods {
    width: 100px;
    vertical-align: middle;
  }
  .btn-text {
    color: #409eff;
    font-size: 14px;
    cursor: pointer;
  }
  .placeholder {
    color: #555;
    line-height: 80px;
    font-size: 24px;
  }
  
</style>

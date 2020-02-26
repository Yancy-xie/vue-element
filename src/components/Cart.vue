<template>
  <div class="content">
    <el-table
      class="el-table"
      ref="multipleTable"
      :data="cart"
      tooltip-effect="dark"
      style="width: 100%"
       @selection-change="handleSelectionChange"
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
          <el-input-number
            size="mini"
            v-model="scope.row.quantity"
            :min="1"
            controls-position="right"
          ></el-input-number>
        </template>
      </el-table-column>
      <el-table-column prop="sum" label="金额" width="160">
        <template slot-scope="scope">￥{{ scope.row.price * scope.row.quantity }}</template>
      </el-table-column>
      <el-table-column label="操作" width="200">
        <template slot-scope="scope">
          <el-button @click="drop(scope.$index)" type="text" size="small">删除</el-button>
          <el-button
            @click="pay(scope.row, scope.index)"
            type="text"
            size="small"
          >结算</el-button>
        </template>
      </el-table-column>
    </el-table>
    <el-row>
      <el-col span="21">
     <div class="row-1"><span>￥&nbsp;{{ getTotalPrice() }}</span>&nbsp;&nbsp;&nbsp;&nbsp;</div>
     </el-col>
     <el-col span="3">
     <el-button class="el-row-button" @click="payAll">结算</el-button>
     </el-col>
    </el-row>
    <table class="table-goods" v-if="cart.length"></table>
    <div class="placeholder" v-else>购物车里还没有东西哦！快去添加吧~~</div>
  </div>
</template>

<script>
import Checkbox from "@/widgets/Checkbox";
export default {
  name: "Cart",
  components: { Checkbox },
  data() {
    return {
      isAllChecked: false,
      checkedArray: [],
      cart: [],
      order: [],
      multipleSelection: []
    };
  },
  mounted() {
    this.$nextTick(function() {
      this.getStore();
      this.setCheckedArray();
    });
  },
  methods: {
     handleSelectionChange(val) {
        this.multipleSelection = val;
      },
    getStore() {
      let gsStore = window.localStorage.getItem("gsStore");
      if (gsStore) {
        gsStore = JSON.parse(gsStore);
        this.cart = gsStore.cart || [];
        this.order = gsStore.order || [];
      }
    },
    setStore() {
      let gsStore = {
        cart: this.cart,
        order: this.order
      };
      window.localStorage.setItem("gsStore", JSON.stringify(gsStore));
    },
    setCheckedArray() {
      this.checkedArray = this.cart.map(() => false);
    },
    getTotalPrice() {
      let balance = this.cart.filter((item, index) => this.multipleSelection[index]);
      return balance.reduce((sum, item) => sum + item.price * item.quantity, 0);
    },
    onCheckChanged() {
      this.checkedArray.every(item => item) && (this.isAllChecked = true);
      this.checkedArray.some(item => !item) && (this.isAllChecked = false);
    },
    onAllCheckChanged() {
      this.checkedArray.fill(this.isAllChecked);
    },
    toggleQuantity() {
      this.setStore();
    },
    drop(index) {
      this.cart.splice(index, 1);
      this.checkedArray.splice(index, 1);
      this.setStore();
    },
    pay(item, index) {
      console.log(11);
      console.log(item);
      this.cart.splice(index, 1);
      this.checkedArray.splice(index, 1);
      this.order.push(item);
      this.setStore();
    },
    payAll() {
      let inCart = [];
      this.checkedArray.forEach((item, index) => {
        item
          ? this.order.push(this.cart[index])
          : inCart.push(this.cart[index]);
      });
      this.cart = inCart;
      this.setCheckedArray();
      this.setStore();
    }
  }
};
</script>

<style scoped>
.content {
  width: 1120px;
  margin-left: auto;
  margin-right: auto;
  color: #000000;
}
.row-1{
  float: right;
  font-size:18px;
  vertical-align: middle;
  line-height: 40px;
}
.table-goods > tbody > tr {
  transition: background-color 200ms linear;
  border-top: 1px solid #ebeef5;
}
.table-goods > tbody > tr:hover {
  background-color: rgba(149, 191, 103, 0.1);
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
.el-table {
  text-align: left;
  font-size: 16px;
  padding-left: 12px;
  color: #000000;
}
.el-table-column {
  color: #000000;
}
.el-input-number {
  width: 85px;
}
.el-row-button{
  background-color:rgb(12, 145, 12);
  color: #fff;
  width: 120px;
  float: right;
}
.ipt-quantity {
  width: 60px;
  padding-left: 10px;
  line-height: 32px;
  outline: none;
  border: 1px solid #ccc;
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
.banner-pay {
  border-top: 1px solid #ebeef5;
  padding: 15px 5px;
  overflow: hidden;
  text-align: right;
  color: #777;
}
.btn-pay {
  display: inline-block;
  width: 120px;
  cursor: pointer;
  line-height: 36px;
  text-align: center;
  color: #fff;
  background-color: #95bf47;
  user-select: none;
  transition: background-color 0.2s linear;
}
.placeholder {
  color: #555;
  line-height: 80px;
  font-size: 24px;
}
</style>

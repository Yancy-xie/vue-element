<template>
  <div>
    <div class="gs-header">
      <el-row :gutter="20">
  <el-col :span="6" :offset="1">
    <div class="gs-nav-item">
        <span>你好，游客</span>&nbsp;&nbsp;&nbsp;&nbsp;
        <span>消息 <strong>0</strong></span>
    </div>
    </el-col>
  <el-col :span="6" :offset="11">
    <div class="gs-nav-item">
       <router-link class="gs-link" to="/order">我的订单</router-link>&nbsp;&nbsp;
         <router-link class="gs-link" to="/cart">
              <i class="el-icon-shopping-cart-full"></i>&nbsp;购物车
            </router-link>&nbsp;&nbsp;
           <span class="gs-link gs-forbid">收藏夹</span>  &nbsp;&nbsp;
            <span class="gs-link gs-forbid">商家入口</span>
      </div>
      </el-col>
</el-row>
 <el-row :gutter="20">
  <el-col :span="6" :offset="1" class="gs-logo" @click="toHomepage">
    <!-- <router-link to="/path"></router-link> -->
    </el-col>
  <el-col :span="6" :offset="11">
   <div style="margin-top: 30px">
    <el-input class="el-input" placeholder="请输入 商品/店铺" v-model="input2">
       <template slot="append"><span >搜&nbsp;&nbsp;索</span></template>
    </el-input>
     </div>
      </el-col>
</el-row>
    </div>
    <router-view/>
  </div>
</template>

<script>
  export default {
    name: 'App',
      data() {
    return {
      input2: '',
    }
    },
    methods: {
      toHomepage () {
        this.$router.push('/')
      }
    }
  }
</script>

<style>
  .gs-link {
    color: #999;
    text-decoration: none;
    outline: none;
  }
  .gs-forbid {
    cursor: not-allowed;
  }
  .gs-menu-bg {
    padding-top: 5px;
    position: absolute;
    width: 1550px;
    height: 30px;
    background-color: #f2f2f2;
    border-bottom: 1px solid #e5e5e5;
  }
  .gs-quick-menu {
    position: relative;
    font-size: 12px;
    color: #999;
    background-color: #f2f2f2;
  }
  .gs-profile {
    display: inline-block;
    line-height: 30px;
    cursor: pointer;
  }
  .gs-nav {
    position: absolute;
    right: 0;
    display: inline-block;
    line-height: 30px;
    list-style: none;
  }
  .gs-nav-item {
    text-align: right;
    margin-top: 10px;
    margin-bottom: 10px;
    display: inline-block;
  }
  .gs-logo {
    display: inline-block;
    margin-top: 10px;
    margin-bottom: 10px;
    width: 188px;
    height: 75px;
    cursor: pointer;
    background-image: url(./assets/images/logo.png);
    background-repeat: no-repeat;
    background-size: cover;
  }
  .gs-search-box {
    display: inline-block;
    line-height: 100px;
    float: right;
  }
  .gs-search-input {
    box-sizing:border-box;
    width: 260px;
    line-height: 32px;
    padding-left: 6px;
    outline: none;
    border: 2px solid #95bf47;
    vertical-align: middle;
  }
  .gs-search-btn {
    display: inline-block;
    line-height: 36px;
    padding-left: 16px;
    padding-right: 16px;
    color: #fff;
    font-weight: 600;
    background-color: #95bf47;
    vertical-align: middle;
    cursor: pointer;
    user-select: none;
  }
</style>

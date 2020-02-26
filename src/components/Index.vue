<template>
  <div class="container">
    <el-row class="banner">
      <el-col :span="4">
        <el-menu
          default-active="2"
          class="el-menu-vertical-demo"
          background-color="#545c64"
          text-color="#fff"
          active-text-color="#ffd04b"
          v-for="(item, index) in navbars" >
          <el-menu-item index="1">
            <i class="el-icon-menu"></i>
            <span slot="title">&nbsp;&nbsp;{{ item.text }}</span>
          </el-menu-item>
        </el-menu>
      </el-col>
      <el-col :span="20">
        <div class="swiper">
          <Swiper :slides="slidesImage" v-model="index"></Swiper>
        </div>
      </el-col>
    </el-row>
    <el-row class="rec-banner">
      <h1 class="banner-title">精品推荐</h1>
      <el-col
        class="card"
        :span="5"
        v-for="(item, index) in goods"
        :key="index"
        :offset="index > 0 ? 1:0"
      >
        <el-card  class="el-card" >
          <div @click="togglePage(item)">
            <img class="rec-media" :src="item.cover" />
          </div>
          <div class="rec-profile">
            <h4>{{ item.text }}</h4>
          </div>
          <div class="rec-params">
            原价:
            <span class="rec-price">￥{{ item.price }}</span>&nbsp;<br>
            促销价:
            <span class="rec-online-price">￥{{ item.onlinePrice }}</span>
          </div>
        </el-card>
      </el-col>
    </el-row>
  </div>
</template>

<script>
import Swiper from "@/widgets/Swiper";
import config from "@/config/config";
export default {
  name: "Index",
  components: { Swiper },
  data() {
    return {
      index: 0
    };
  },
  computed: {
    navbars() {
      return config.navbars;
    },
    goods() {
      return config.goods;
    },
    slidesColor() {
      return config.goods.map(item => item.color);
    },
    slidesImage() {
      return config.goods.map(item => item.poster);
    }
  },
  methods: {
    togglePage(item) {
      this.$router.push({ path: "goods", query: { name: item.name } });
    }
  }
};
</script>

<style scoped>
.container {
  position: relative;
  background-color: #f5f5f5;
  border-bottom: 1px solid transparent;
}
.card {
  margin-left: 18px;
  margin-right: 20px;
  text-align: center;
}
.swiper {
  height: 500px;
  background-color: #e8e8e8;
}
.rec-banner {
  margin: 30px auto;
  padding-top: 30px;
  padding-bottom: 50px;
  width: 1120px;
  background-color: #fff;
}
.banner-title {
  padding: 8px 15px;
}
.el-card {
  padding:10px 2px;
}
.rec-list {
  list-style: none;
}
.rec-card {
  display: inline-block;
  width: 25%;
  text-align: center;
  vertical-align: top;
  cursor: pointer;
}
.rec-media {
  width: 210px;
}
.rec-profile {
  text-align: center;
  width: 200px;
  display: inline-block;
  color: #444;
}
.rec-price {
  text-decoration: line-through;
}
.rec-online-price {
  color: #ff0036;
  font-size: 16px;
}
.rec-params {
  font-size: 12px;
  color: #888;
}
.el-menu-item{
  line-height: 34px
}
.el-menu{
 height:34px
}
</style>

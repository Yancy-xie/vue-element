<template>
  <el-carousel height="500px" indicator-position="outside">
    <el-carousel-item v-for="(img,index) in imgList" :key="index">
      <img v-bind:src="img.url" />
    </el-carousel-item>
  </el-carousel>
</template>

<style>
.el-carousel__item h3 {
  color: #475669;
  font-size: 18px;
  opacity: 0.75;
  line-height: 500px;
  margin: 0;
}
.el-carousel__item:nth-child(2n) {
  background-color: #99a9bf;
}
.el-carousel__item:nth-child(2n + 1) {
  background-color: #d3dce6;
}
</style>
<script>
export default {
  data() {
    return {
      imgList: [
        {
          url: "./static/images/slide01.png"
        },
        {
          url: "./static/images/slide02.png"
        },
        {
          url: "./static/images/slide03.png"
        }
      ]
    };
  }
};
</script>

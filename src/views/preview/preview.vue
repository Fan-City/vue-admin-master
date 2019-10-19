<template>
  <div>
    <h1>preview 点击按钮放大测试</h1>
    <img :src="imgSrc" preview preview-text="描述文字">
    <!-- <img :src="imgSrc2" preview="0" preview-text="描述文字"> -->
    <el-button @click="fangda"></el-button>
  </div>
</template>

<script>
import { setTimeout } from 'timers';
export default {
  data(){
    return {
      imgSrc: 'https://ss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=1130583636,2033493811&fm=27&gp=0.jpg',
      imgSrc2: 'https://ss3.bdstatic.com/70cFv8Sh_Q1YnxGkpoWK1HF6hhy/it/u=877901702,1386033979&fm=27&gp=0.jpg'
    }
  },
  // computed:{
  //   Swiper
  // },
  created(){

  },
  mounted() {
  },
  methods:{
    fangda(){
      // console.log(this.$preview)
      var that = this
      // that.$preview.init()
      this.$preview.on('imageLoadComplete',(e,item)=>{
        console.log(that.$preview.self)  //此时this.$preview.self拥有原插件photoswipe文档中的所有方法和属性
      })
      console.log(that.$preview.self)
      that.$preview.self.init()
      // this.$preview.self.toggleDesktopZoom()
    }
  }
}

</script>
<style  scoped>
.swiper-container-thumbs {
    /* width: 500px; */
    height: 300px;
    margin: 20px auto;
}
.bg{
  width: 300px;
  height: 200px;
  border: 1px solid;
  text-align: center;
}
.my-slide-thumb-active .bg{
  border: 1px solid #e42020;
}
</style>

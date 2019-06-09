<template>
  <div>
    <h1>swiper 轮播测试</h1>
    <div class="swiper-container1">
      <div class="swiper-wrapper">
        <div class="swiper-slide" v-for="(item,index) in imageList" :key="index" :data-index="index">
          <div class="bg" :data-index="index">
            {{item}}
          </div>
        </div>
      </div>
    </div>
    <div class="swiper-container-thumbs">
      <div class="swiper-wrapper">
        <div class="swiper-slide" v-for="(item,index) in imageList" :key="index" :data-index="index">
          <div class="bg" :data-index="index">
            {{item}}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Swiper from 'swiper';
import 'swiper/dist/css/swiper.min.css';
import { setTimeout } from 'timers';
export default {
  data(){
    return {
      imageList: ['slider1',
                  'slider2',
                  'slider3',
                  'slider4',
                  'slider5',],
      mySwiper: null,
      mySwiper1: null
    }
  },
  // computed:{
  //   Swiper
  // },
  created(){

  },
  mounted() {
    var that = this 
    that.$nextTick(function(){
      that.mySwiper = new Swiper ('.swiper-container-thumbs', {
        spaceBetween: 10,
        watchSlidesVisibility: true,
        // loop: true,
        slidesPerView: 3.5,
        // slidesPerview:'auto',
        freeMode : true,
        spaceBetween: 10,
        slideToClickedSlide: false
      })

      that.mySwiper1 = that.mySwiper = new Swiper ('.swiper-container1', {
        autoplay: {
          delay: 2000,//1秒切换一次
        },
        loop: true,
        thumbs: {
          swiper: that.mySwiper,
          slideThumbActiveClass: 'my-slide-thumb-active'
          // swiper: {
          //   el: '.swiper-container-thumbs',
          //   slidesPerView: 3.5
          // }
        }
      })
    });
    
  },
  methods:{
    aaaaa:function(){
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

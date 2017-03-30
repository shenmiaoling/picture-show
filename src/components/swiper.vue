<template>
  <div class="swiper-container">
    <div class="swiper-wrapper">
      <router-link to="/preview" class=
      'swiper-slide'>
        <div style="background-image:url(http://lorempixel.com/1000/1000/nightlife/1)"></div>
      </router-link>

        <div class="swiper-slide" style="background-image:url(http://lorempixel.com/1000/1000/nightlife/2)"></div>
        <div class="swiper-slide" style="background-image:url(http://lorempixel.com/1000/1000/nightlife/3)"></div>
        <div class="swiper-slide" style="background-image:url(http://lorempixel.com/1000/1000/nightlife/4)"></div>
        <div class="swiper-slide" style="background-image:url(http://lorempixel.com/1000/1000/nightlife/5)"></div>
    </div>
    <!-- Add Pagination -->
    <div class="swiper-pagination swiper-pagination-white"></div>
    <!-- Add Arrows -->
    <div class="swiper-button-next swiper-button-white"></div>
    <div class="swiper-button-prev swiper-button-white"></div>
  </div>
</template>
<script>
  import Swiper from 'swiper'
  import 'swiper/dist/css/swiper.min.css'
  export default{
    mounted(){
    var swiper = new Swiper('.swiper-container', {
        pagination: '.swiper-pagination',
        paginationClickable: true,
        nextButton: '.swiper-button-next',
        prevButton: '.swiper-button-prev',
        spaceBetween: 30,
        effect: 'fade',
        // autoplay: 2500,
        // autoplayDisableOnInteraction: false
    });
    }
  }
</script>
<style lang="styl">
  .router
    display block
    width 100%
    /*height 200px*/
  html, body {
      position: relative;
      height: 100%;
  }
  body {
      background: #eee;
      font-family: Helvetica Neue, Helvetica, Arial, sans-serif;
      font-size: 14px;
      color:#000;
      margin: 0;
      padding: 0;
  }
  .swiper-container {
      width: 100%;
      height: 200px!important;
  }
  .swiper-slide {
      background-position: center;
      background-size: cover;
      height: 100%!important
  }
</style>

<template>
  <div>
    <nv-head page-type="首页"
     :go-back="false"></nv-head>
    <nv-swiper></nv-swiper>
  </div>
</template>
<script>
  import nvHead from '../components/header.vue'
  import nvSwiper from '../components/swiper.vue'
  export default {
    components:{
      nvHead,
      nvSwiper
    }
  }
</script>

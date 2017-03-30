<template>
  <div>
    <nv-head></nv-head>
    <nv-swiper></nv-swiper>
    <router-link to="/preview">
      <button>preview</button>
    </router-link>
  </div>
</template>
<script>
  import nvHead from '@/components/header.vue'
  import nvSwiper from '@/components/swiper.vue'
  export default {
    components:{
      nvHead,
      nvSwiper
    }
  }
</script>

<style lang="styl">
  .icon-back
    position: absolute;
    top: 10px;
    left: 5px;
    font-size: 20px;
  header
    text-align center
    padding 10px
    font-weight bold
    background-color #fff
    box-shadow: 0 3px 6px rgba(0,0,0,0.16), 0 0 6px rgba(0,0,0,0.23);
</style>
<template>
  <div>
    <span class="iconfont icon-back" v-show="goBack" @click="$router.push('/')"></span>
    <header v-text="pageType">
    </header>
  </div>

</template>
<script>
  export default {
    props: ['pageType','goBack']
  }
</script>

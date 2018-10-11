<template>
  <transition name="slide-down">
    <div class="title_container" v-show="showMenu">
      <div class="left">
        <span class="icon-back icon"></span>
      </div>
      <div class="right">
        <span class="icon-cart icon"></span>
        <span class="icon-person icon"></span>
        <span class="icon-more icon"></span>
      </div>
    </div>
  </transition>
</template>

<script>
  export default {
    props:{
      showMenu:{
        type:Boolean,
        default:false
      }
    }
  }
</script>
<style lang="scss" scoped>
  @import '../assets/style/global';

  .title_container{
    display: flex;
    position: absolute;
    top: 0;
    left: 0;
    z-index: 101;
    width: 100%;
    height: px2rem(48);
    background: white;
    box-shadow: 0 px2rem(5) px2rem(8) rgba(0,0,0,.15);
    justify-content: space-between;
    padding: 0 px2rem(10);

    .right{
      .icon-cart{
        font-size: px2rem(21);
      }
    }
  }


</style>


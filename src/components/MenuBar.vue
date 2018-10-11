<template>
  <div class="menu-bar">
    <transition name="slide-up">
      <div class="setting-bar" v-show="ifShowSetting">
        <div class="setting-font-size"></div>
      </div>
    </transition>
    <transition name="slide-up">
      <div class="foot_container" v-show="showMenu">
        <span class="icon-menu icon"></span>
        <span class="icon-progress icon"></span>
        <span class="icon-bright icon" @click="showSetting"></span>
        <span class="icon-share icon"></span>
      </div>
    </transition>
  </div>
</template>

<script>
  export default {
    props:{
      showMenu:{
        type:Boolean,
        default:false
      }
    },

    data() {
      return {
        ifShowSetting:false
      }
    },

    methods: {
      showSetting() {
        this.ifShowSetting = true
      },
      hideSetting() {
        this.ifShowSetting = false
      }
    }
  }
</script>
<style lang="scss" scoped>
  @import '../assets/style/global';

  .menu-bar{

    .foot_container{
      position: absolute;
      width: 100%;
      left: 0;
      bottom: 0;
      display: flex;
      justify-content: space-around;
      align-items: center;
      height: px2rem(48);
      background: white;
      box-shadow: 0 px2rem(-3) px2rem(8) rgba(0,0,0,.15);
    }

    .setting-bar{
      position: absolute;
      width: 100%;
      left: 0;
      bottom: 0;
      height: px2rem(96);
      background: white;
      box-shadow: 0 px2rem(-3) px2rem(8) rgba(0,0,0,.15);

      .setting-font-size{

      }
    }
  }
</style>

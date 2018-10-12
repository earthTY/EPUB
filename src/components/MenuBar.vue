<template>
  <div class="menu-bar">
    <transition name="slide-up">
      <div class="setting-bar" v-show="ifShowSetting">
        <SettingFontSize v-if="showSettingTag === 2" :fontSizeList="fontSizeList" :defaultFontSize="defaultFontSize" @settingFontSize="settingFontSize"/>
        <div v-else-if="showSettingTag === 3" class="setting-themes">
          <div class="preview" v-for="(val,index) in themesList">
            <div class="theme-color" :class="{active:defaultTheme === index}" :style="{background:val.style.body.background}"></div>
            <div class="theme-name"  :class="{active:defaultTheme === index}">{{val.name}}</div>
          </div>
        </div>
      </div>
    </transition>
    <transition name="slide-up">
      <div class="foot_container" v-show="showMenu" :class="{'hideBoxShodow':ifShowSetting}">
        <span class="icon-menu icon"></span>
        <span class="icon-progress icon"></span>
        <span class="icon-bright icon" @click="showSetting(2)"></span>
        <span class="icon-share icon" @click="showSetting(3)"></span>
      </div>
    </transition>
  </div>
</template>

<script>
  import SettingFontSize from "@/components/menubar/SettingFontSize"
  export default {
    props:{
      showMenu:{
        type:Boolean,
        default:false
      },

      //设置字体大小
      fontSizeList:{
        type:Array
      },
      defaultFontSize:{
        type:Number
      },

      //设置主题
      defaultTheme:{
        type:Number
      },
      themesList:{
        type:Array
      }
    },

    components:{
      SettingFontSize
    },

    data() {
      return {
        ifShowSetting:false,
        showSettingTag:0
      }
    },

    methods: {
      showSetting(tagIndex) {
        this.showSettingTag = tagIndex
        this.ifShowSetting = true
      },
      hideSetting() {
        this.ifShowSetting = false
      },
      settingFontSize(fontSize) {
        this.$emit("settingFontSize",fontSize)
      }
    }
  }
</script>
<style lang="scss" scoped>
  @import '../assets/style/global';

  .menu-bar{

    .setting-themes{
      display: flex;
      height: px2rem(48);

    .preview{
      flex: 1;
      display: flex;
      flex-direction: column;

      .theme-color{
        flex: 1;
        margin: px2rem(5);

        &.active{
           border: 1px solid #cccddd;
         }
      }
      .theme-name{
        flex: 0 0 px2rem(16);
        font-size: px2rem(12);
        @include center;

        &.active{
           font-weight: bold;
         }
      }
    }

  }

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

  &.hideBoxShodow{
     box-shadow: none;
   }
  }

  .setting-bar{
    position: absolute;
    width: 100%;
    left: 0;
    bottom: 0;
    height: px2rem(96);
    background: white;
    box-shadow: 0 px2rem(-3) px2rem(8) rgba(0,0,0,.15);
  }
  }
</style>

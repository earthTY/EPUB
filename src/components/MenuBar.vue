<template>
  <div class="menu-bar">
    <transition name="slide-up">
      <div class="setting-bar" v-show="ifShowSetting">
        <div class="setting-progress" v-if="showSettingTag === 1">
          <div class="progress-wrapper" v-if="loadProgress">
            <input type="range" v-model="progress" @input="onChangeProgress" @change="onChangeProgress" ref="progress"/>
          </div>
          <div v-else>加载中...</div>
        </div>
        <SettingFontSize v-else-if="showSettingTag === 2" :fontSizeList="fontSizeList" :defaultFontSize="defaultFontSize" @settingFontSize="settingFontSize"/>
        <SettingThemes v-else-if="showSettingTag === 3" :themesList="themesList" :defaultTheme="defaultTheme" @setTheme="setTheme"/>
      </div>
    </transition>
    <transition name="slide-up">
      <div class="foot_container" v-show="showMenu" :class="{'hideBoxShodow':ifShowSetting}">
        <span class="icon-menu icon"></span>
        <span class="icon-progress icon" @click="showSetting(1)"></span>
        <span class="icon-share icon" @click="showSetting(2)"></span>
        <span class="icon-bright icon" @click="showSetting(3)"></span>
      </div>
    </transition>
  </div>
</template>

<script>
  import SettingFontSize from "@/components/menubar/SettingFontSize"
  import SettingThemes from "@/components/menubar/SettingThemes"
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
      },

      loadProgress:{
        type:Boolean
      },
    },

    components:{
      SettingFontSize,
      SettingThemes
    },

    data() {
      return {
        ifShowSetting:false,
        showSettingTag:0,
        progress:0,
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
      },
      setTheme(index){
        this.$emit("setTheme",index)
      },
      onChangeProgress(){
        this.$refs.progress.style.backgroundSize=this.progress+'% 100%'
        this.$emit("onChangeProgress",this.progress)
      }
    }
  }
</script>
<style lang="scss" scoped>
  @import '../assets/style/global';

  .menu-bar{
    .setting-progress{
      padding: 0 px2rem(20);
      @include center;
      height: px2rem(48);
      font-size: px2rem(16);

      .progress-wrapper{
        width: 100%;
        input[type=range]{

          -webkit-appearance: none;
          /*清除系统默认样式*/
          width: 100%;
          background: -webkit-linear-gradient(#747474,#747474) no-repeat #cccccc;
          /*设置左边颜色为#61bd12，右边颜色为#ddd*/
          /*设置左右宽度比例*/
          height: 3px;
          /*横条的高度*/
          outline: none;
        }

        input[type=range]::-webkit-slider-thumb {
          -webkit-appearance: none;
          /*清除系统默认样式*/
          height: px2rem(20);
          /*拖动块高度*/
          width: px2rem(20);
          /*拖动块宽度*/
          background: #fff;
          border: 1px solid #cccddd;
          border-radius: 50%;
          /*拖动块背景*/
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

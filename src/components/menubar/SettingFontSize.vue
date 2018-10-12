<template>
  <div class="setting-font-size">
    <div class="preview" :style="{fontSize:fontSizeList[0]+'px'}">A</div>
    <div class="setting-wrapper">
      <div class="setting-item" v-for="(item,index) in fontSizeList" @click="settingFontSize(item)">
        <div class="through"></div>
        <div class="line"></div>
        <div class="print-wrapper" v-show="item === defaultFontSize">
          <div class="point">
            <div class="small"></div>
          </div>
        </div>
        <div class="through"></div>
      </div>
    </div>
    <div class="preview" :style="{fontSize:fontSizeList[fontSizeList.length - 1]+'px'}">A</div>
  </div>
</template>

<script>
  export default {
    props:{
      fontSizeList:{
        type:Array
      },
      defaultFontSize:{
        type:Number
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
      },
      settingFontSize(fontSize) {
        this.$emit("settingFontSize",fontSize)
      }
    }
  }
</script>
<style lang="scss" scoped>
  @import '../../assets/style/global';

  .setting-font-size{
    display: flex;
    height: px2rem(48);

    .preview{
      flex: 0 0 px2rem(40);
      @include center;
    }
    .setting-wrapper{
      display: flex;
      flex: 1;

      .setting-item{
        flex: 1;
        display: flex;
        align-items: center;

        .through{
          flex: 1;
          border-top: 1px solid #cccddd;
          height: 0;
        }
        .line{
          height: px2rem(5);
          width: px2rem(1);
          background: #cccddd;
          @include center;
        }

      .print-wrapper{
        position: relative;
        .point{
            position: absolute;
            top:px2rem(-8);
            left:px2rem(-8);
            width:px2rem(16);
            height:px2rem(16);
            border:1px solid #cccddd;
            border-radius:50%;
            box-shadow: 0 0 px2rem(8) rgba(0,0,0,.15);
            @include center;

            .small{
              width:px2rem(5);
              height:px2rem(5);
              background: #000000;
              border-radius:50%;
            }
          }
        }

        &:first-child{
          div:first-child{
            border-top: 0;
          }
        }

        &:last-child{
          div:last-child{
            border-top: 0;
          }
        }
      }
    }
  }
</style>

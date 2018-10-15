<template>
  <div v-else-if="showSettingTag === 3" class="setting-themes">
    <div class="preview" v-for="(val,index) in themesList">
      <div class="theme-color" :class="{active:defaultTheme === index}" :style="{background:val.style.body.background}" @click="setTheme(index)"></div>
      <div class="theme-name"  :class="{active:defaultTheme === index}">{{val.name}}</div>
    </div>
  </div>
</template>

<script>
  export default {
    props:{
      //设置主题
      defaultTheme:{
        type:Number
      },
      themesList:{
        type:Array
      }
    },

    methods: {
      setTheme(index){
        this.$emit("setTheme",index)
      }
    }
  }
</script>
<style lang="scss" scoped>
  @import '../../assets/style/global';

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
</style>

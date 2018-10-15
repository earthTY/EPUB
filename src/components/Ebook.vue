<template>
  <div class="ebook">
    <TitleBar :showMenu="showMenu"/>
    <div class="book_container">
      <div id="read">
      </div>
      <div class="topView">
        <div class="viewleft" @click="prevPage"></div>
        <div class="center" @click="toggleShowMenu"></div>
        <div class="viewright" @click="nextPage"></div>
      </div>
    </div>
    <MenuBar :showMenu="showMenu"
             :defaultTheme="defaultTheme"
             :themesList="themesList"
             @settingFontSize="settingFontSize"

             :fontSizeList="fontSizeList"
             :defaultFontSize="defaultFontSize"
             @setTheme="setTheme"

             :loadProgress="loadProgress"
             @onChangeProgress="onChangeProgress"

             ref="menuBar"/>
  </div>
</template>

<script>
  import TitleBar from "@/components/TitleBar"
  import MenuBar from "@/components/MenuBar"
  import Epub from 'epubjs'
  const EPUB_URL = "/static/197803.epub"
  export default {
    components:{
      TitleBar,
      MenuBar
    },
    data() {
      return {
        showMenu: false,

        fontSizeList: [12,14,16,18,20,22,24],

        defaultFontSize:16,

        themesList: [
          {
            name:"默认",
            style:{
              'body':{
                color:'#000',
                background:'#fff'
              }
            }
          },
          {
            name:"护眼",
            style:{
              'body':{
                color:'#000',
                background:'#3a8a16'
              }
            }
          },
          {
            name:"夜间",
            style:{
              'body':{
                color:'#fff',
                background:'#000'
              }
            }
          },
          {
            name:"高亮",
            style:{
              'body':{
                color:'#000',
                background:'#fea'
              }
            }
          }
        ],

        defaultTheme:0,

        loadProgress:false,
      }
    },
    mounted() {
      this.showEpub()

      var that = this
      window.onresize=function() {
        that.showEpub()
      }
    },
    methods: {
      showEpub() {
        //创建Epub对象
        this.book = new Epub(EPUB_URL)

        document.getElementById("read").innerHTML = ""

        this.radition = this.book.renderTo("read", {width: window.innerWidth, height: window.innerHeight});

        this.themes = this.radition.themes

        this.themes.fontSize(this.defaultFontSize + "px")



        var that = this
        this.themesList.forEach((theme)=>{
          this.themes.register(theme.name,theme.style)
        })

        this.setTheme(this.defaultTheme)

        this.radition.display()

        this.book.ready.then(()=>{
           return this.book.locations.generate()
        }).then((result) => {
          this.loadProgress = true
          this.locations = this.book.locations
        })
      },
      onChangeProgress(progress){
        var progress = progress / 100

        var location = progress > 0 ? this.locations.cfiFromPercentage(progress) : 0

        this.radition.display(location)
      },
      prevPage() {
        if(this.radition){
          this.radition.prev()
        }
      },
      nextPage() {
        if(this.radition){
          this.radition.next()
        }
      },
      toggleShowMenu() {
        this.showMenu = !this.showMenu

        if(!this.showMenu){
          this.$refs.menuBar.hideSetting()
        }
      },
      settingFontSize(fontSize) {
        this.defaultFontSize = fontSize
        if(this.themes){
          this.themes.fontSize(fontSize + "px")
        }
      },
      setTheme(index) {
        this.defaultTheme = index
        this.themes.select(this.themesList[index].name)
      }
    }
  }

</script>
<style lang="scss" scoped>
  @import '../assets/style/global';

  .book_container{
    position: relative;
    width: 100%;
    overflow: hidden;


    .topView{

      display: flex;
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;

      .viewleft{
        flex: 0 0 px2rem(100);
      }
      .center{
        flex: 1;
      }
      .viewright{
        flex: 0 0 px2rem(100);
      }
    }
  }

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

  .foot_container{
    position: absolute;
    left: 0;
    bottom: 0;
    width: 100%;
    display: flex;
    justify-content: space-around;
    align-items: center;
    height: px2rem(48);
    background: white;
    box-shadow: 0 px2rem(-3) px2rem(8) rgba(0,0,0,.15);
  }


</style>

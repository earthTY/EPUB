<template>
  <div class="ebook">
    <div class="book_container">
      <div id="read">
      </div>
      <div class="topView">
        <div class="viewleft" @click="prevPage"></div>
        <div class="center"></div>
        <div class="viewright" @click="nextPage"></div>
      </div>
    </div>
  </div>
</template>

<script>
  import Epub from 'epubjs'
  const EPUB_URL = "/static/197803.epub"
  export default {
    created() {
      this.showEpub()
    },
    methods: {
      showEpub() {
        //创建Epub对象
        this.book = new Epub(EPUB_URL)

        this.radition = this.book.renderTo("read", {width: window.innerWidth, height: window.innerHeight});

        this.radition.display()
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
      }
    }
  }

</script>

<style lang="scss" scoped>
  @import '../assets/style/global';

  .book_container{
    position: relative;

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
</style>

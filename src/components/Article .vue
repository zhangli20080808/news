<template>
  <div id="article">
    <mt-header>
      <router-link to="/" slot="left">
        <mt-button icon="back">返回</mt-button>
      </router-link>
    </mt-header>
    <div class="header">
      <div class="header_img"><img src="../assets/images/1.jpeg" alt="">
        <h2 class="text">{{articleData.author}}</h2>
      </div>
      <div class="content">
        <h3>{{articleData.title}}</h3>
        <hr>
        <div class="time">
          <p class="time">{{articleData.time | normalData}}</p>
          <span></span>
        </div>
        <div class="text_content">
          <p v-html="articleData.content"></p>
        </div>

      </div>

    </div>
  </div>
</template>
<script>

  export default {
    name: 'app',
    data(){
      return {
        articleData: [],
      }
    },
    mounted(){
      var reg = /\/article\/(\d+)/;
      var id = this.$route.path.match(reg)[1];
      this.fetchData(id)
    },
    methods: {
      fetchData: function (id) {
        var _this = this;
        this.$http({
          method: 'post',
          url: '/api/json/article.json',
          headers: {'Content-Type': 'application/json', 'Accept': 'application/json'}
        }).then((res) => {
//          console.log(res)
          _this.articleData = res.data[id - 1];
        }).catch(function (err) {
          console.log('文章详情页面:', err)
        })
      }
    }
  }


</script>
<style scoped lang="less">
  #article {
    background: rgba(30, 37, 68, 0.09);
    .header {
      .header_img {
        padding-left: 20px;
        height: 80px;
        line-height: 80px;
        /*垂直对齐文本的上标*/
        vertical-align: super;
        img {
          width: 40px;
          height: 40px;
          border-radius: 50%;
          vertical-align: middle;
        }
        .text {
          display: inline-block;
          padding-left: 20px;
          font-size: 24px;
        }
      }
      .content {
        font-size: 20px;
        width: 92%;
        margin-left: auto;
        margin-right: auto;
        min-height: 100%;
        padding: 20px 10px;
        .time {
          .time{
            margin: 15px 0;
          }
        }
        .text_content{
          p{
            margin: 20px 0;
            line-height: 2;
            font-size: 14px;
          }
        }
      }
    }
  }

</style>

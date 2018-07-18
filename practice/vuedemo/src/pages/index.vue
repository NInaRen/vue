<template>
  <div class="index">
    <div class="left">
      <div class="class-wrap">
        <div class="title">全部产品</div>
        <template v-for="product in productList">
          <div class="class-item">
            <div class="class-title">{{ product.name}}</div>
            <ul>
              <li v-for="item in product.list">
                <a :href="item.url">{{ item.title }}</a>
                <span v-if="item.hot" class="hot-tag">HOT</span>
              </li>
            </ul>
          </div>
        </template>

        <div class="line-space"></div>

        <div class="title">最新消息</div>
        <div class="class-item news-list">
          <ul>
            <li v-for="item in newsList">
              <a :href="item.url" class="new-item">{{ item.title }}</a>
              <span v-if="item.hot" class="hot-tag">HOT</span>
            </li>
          </ul>
        </div>
      </div>
    </div>
    <div class="right">
      <div class="index-top">
        <slider-show :slides="slides" :itvTime="itvTime"></slider-show>
      </div>
      <div class="index-bottom">
        <template v-for="(item, index) in boardList">
          <div class="item-box">
            <div :class="'index-img-' + item.id"></div>
            <div class="content-tag">
              <p>{{item.name}}</p>
              <p>{{item.description}}</p>
              <div class="index-board-button">
                <router-link class="button" :to="{path: 'detail/' + item.toKey}">立即购买</router-link>
              </div>
            </div>
          </div>
          <span v-if="index % 2 === 0" class="span-space"></span>
        </template>
      </div>

    </div>
  </div>
</template>

<script>
  import sliderShow from '../components/sliderShow'
  export default {
    components: {
      sliderShow,
    },
    created: function () {
      //学习前端模拟数据获取
      this.$http.get('api/news', {id:2}).then((data)=>{
        this.newsList = data.data.data
      },(err) => {
        console.log(err);
      })
    },
    data () {
      return {
        newsList: [],
        boardList: [
          {
            name: 'hah',
            description: "testestetoiopxdlasdfdgfhjkgia",
            id: 'car',
            toKey: 'publish'
          },
          {
            name: 'hah',
            description: "testestetoiopxdlasdfdgfhjkgia",
            id: 'festival',
            toKey: 'analysis'
          },
          {
            name: 'hah',
            description: "testestetoiopxdlasdfdgfhjkgia",
            id: 'sunny',
            toKey: 'count'
          },
          {
            name: 'hah',
            description: "testestetoiopxdlasdfdgfhjkgia",
            id: 'moving',
            toKey: 'forecast'
          }
        ],
        productList: {
          pc: {
            name: 'PC产品',
            list: [
              {
                title: 'test1',
                url: 'test1'
              },
              {
                title: 'test2',
                url: 'test3'
              },
              {
                title: 'test3',
                url: 'test3',
                hot: true
              },{
                title: 'test4',
                url: 'test4'
              },
              {
                title: 'test5',
                url: 'test5'
              },


            ]
          },
          app: {
            name: 'app产品',
            list: [
              {
                title: '好搭',
                url: 'test1'
              },
              {
                title: '支付宝',
                url: 'test3'
              },
              {
                title: '微信',
                url: 'test3'
              },{
                title: 'keep',
                url: 'test4'
              },
              {
                title: '咪咕',
                url: 'test5'
              },
            ]
          }

        },
        slides: [
          {
            src: require('../assets/slideShow/pic1.jpg'),
            title: 'tell me why',
            href: 'detail/analysis'
          },
          {
            src: require('../assets/slideShow/pic2.jpg'),
            title: 'gona white beautify',
            href: 'detail/count'
          },
          {
            src: require('../assets/slideShow/pic3.jpg'),
            title: 'telephone',
            href: 'detail/publish'
          },
          {
            src: require('../assets/slideShow/pic4.jpg'),
            title: 'you are what you shape',
            href: 'detail/forecast'
          }
          ,
          {
            src: require('../assets/slideShow/pic5.jpg'),
            title: 'me too',
            href: 'detail/count'
          },
          {
            src: require('../assets/slideShow/pic6.jpg'),
            title: 'i am loving with monster',
            href: 'detail/monster'
          }
        ],
        itvTime: 2000,
      }
    },
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .index {
    font-size: 20px;
    width: 100%;
    float: left;
    margin: 40px 0 20px 0;
  }
  .left {
    float: left;
    width: 20%;
 }
  .right {
    float: left;
    width: 78%;
    margin-left: 2%;
  }
  .title {
    color: #FFF;
    background-color: #41b883;
    padding-left: 30px;
    height: 45px;
    line-height: 45px;
    font-size: 20px;
  }
  .class-wrap {
    background-color: #FFF;
  }
  .class-title {
    font-size: 18px;
    font-weight: 700;
    padding: 10px 0 10px 30px;
  }
  .class-item {
    padding-bottom: 10px;
    border-bottom: 2px solid #ccc;
  }
  .class-item ul li{
    padding-left: 40px;
    font-size: 18px;
    height: 30px;
    line-height: 30px;
  }
  .line-space {
    height: 20px;
    background-color: #f0f2f5;
    width: 100%;
  }
  .hot-tag {
    color: red;
    padding-left: 5px;
  }
  .item-box {
    float: left;
    width: 49%;
    padding: 20px 10px;
    box-sizing: border-box;
    background-color: #FFF;
    margin-top: 10px;
    border-radius: 5px;
  }
  div[class^="index-img-"] {
    float: left;
    width: 120px;
    height: 120px;
  }
  .content-tag {
    float: left;
    height: 100px;
    margin-left: 10px;
  }
  .item-box p {
    height: 30px;
    line-height: 30px;
  }
  .index-board-button {
    height:30px;
    background-color: #41b883;
    width: 100px;
    line-height: 30px;
    text-align: center;
    font-size: 18px;
    border-radius: 5px;
    margin-top: 10px;
    padding: 5px;
  }
  .span-space {
    float: left;
    width: 2%;
    height: 30px;
  }
  .index-img-car {
    background: url("../assets/img/demonstration.png") no-repeat center;
  }

  .index-img-festival {
    background: url("../assets/img/reference.png") no-repeat center;
  }

  .index-img-sunny {
    background: url("../assets/img/remote.png") no-repeat center;
  }

  .index-img-moving {
    background: url("../assets/img/side.png") no-repeat center;
  }

  .new-item {
    display: inline-block;
    width: 180px;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
    font-size: 13px;
  }

  .new-item:hover {
    background-color: #92eeeb;
  }

  .news-list {
    min-height: 220px;
  }

</style>

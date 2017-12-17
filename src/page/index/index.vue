<template>
	<div>
      <header class="header">
      	<div class="back iconfont">&#xe624;</div>
      	<div class="search"><a href="#" class="prompt iconfont">&#xe86e;输入城市/景点/游玩主题</a></div>
      	<div class="city iconfont">城市&#xe600;</div>
      </header>

      <swiper :options="swiperOption">
        <swiper-slide v-for="item in swiperInfo" :key="item.id">
          <div class="swiper-img-con">
            <img class="swiper-img" :src="item.imgUrl"/>
          </div>	
        </swiper-slide>
        <div class="swiper-pagination"  slot="pagination"></div>
      </swiper>

      <swiper :options="swiperOptions">
        <swiper-slide v-for="(pageInfo, index) in pages" :key="index">
          <div class="icon-wrapper">
            <div v-for="item in pageInfo" :key="item.id" class="icon-item">
              <div class="icon-img-con">
                <img :src="item.imgUrl" class="icon-img">
              </div>
              <span class="icon-text">{{item.iconInfoText}}</span>
            </div>
          </div>
        </swiper-slide>
        <div class="icon-pagination"  slot="pagination"></div>
      </swiper>

      <div class="promotion-box">
        <div class="promotion-solid"></div>
        <ul class="promotion-box-con">
          <li class="promotion-item">
            <a href="#" class="geolocation iconfont">&#xe60e;定位失败</a>
          </li>
          <div class="promotion-solid-vertical"></div>
          <li class="promotion-item">
            <a href="#" class="hot-spring iconfont">&#xe608;5折泡温泉</a>
          </li>
        </ul>
      </div>
      
      <div class="null-background"></div>
    <div class="discount">
      <ul class="discount-box">
        <li class="discount-water">
          <a href="#"></a>
        </li>
        <div class="promotion-solid-vertical"></div>
        <li class="discount-tickies">
          <a href="#"></a>
        </li>
      </ul>
    </div>
    <div class="page-bottom">
      <div class="sales-recommend">
        <h2>热销推荐</h2>
      </div>
      <div class="hot-bottom">
        <ul class="hot-box">
          <li class="hot-item" v-for="hitem in hotlist" :key="hitem.id">
            <div class="hot-item-box">
              <div class="hot-img-con">
                <img src="hitem.imgUrl">
              </div>
              <div class="hot-introduce">
                <span class="hitem-name">{{hitem.name}}</span>
                <span class="hitem-explain">{{hitem.explain}}</span>
                <span class="hitem-price">{{hitem.price}}</span>
              </div>
          </div>
          </li>
        </ul>
      </div>
    </div>

    <div class="recommend">
      <ul>
        <li></li>
      </ul>
    </div>

	</div>
</template>
<script>
export default {

  name: 'Index',
  data () {
    return {
      swiperInfo: [],
      iconInfo: [],
      iconInfoText: [],
      swiperOption: {
        loop: true,
        pagination: '.swiper-pagination',
        autoplay: 2000
      },
      swiperOptions: {
        pagination: '.icon-pagination'
      }
    }
  },

  methods: {
    getIndexData () {
      this.$http.get('./static/index.json')
        .then(this.handleGetDataSucc.bind(this))
    },

    handleGetDataSucc (res) {
      const body = res.body
      if (body && body.data && body.data.swiper) {
        this.swiperInfo = body.data.swiper
        this.iconInfo = body.data.icons
      }
    }
  },
  computed: {
    pages () {
      const pages = []
      this.iconInfo.forEach((value, index) => {
        let page = Math.floor(index / 8)
        if (!pages[page]) {
          pages[page] = []
        }
        pages[page].push(value)
      })
      return pages
    }
  },
  created () {
    this.getIndexData()
  }
}
</script>
<style scoped>
  .header {
  	display: flex;
  	background: #05bad5;
  	color: #fff;
  }
  .back {
  	width: .64rem;
  	line-height: .86rem;
    text-align: center;
  }
  .search {
  	flex: 1;
  	margin: .14rem .18rem;
  	background: #fff;
  	border-radius: .1rem;
  }
  .prompt {
    font-size: 0.26rem;
    color: #ccc;
    line-height: 0.6rem;
    padding-left:0.15rem;
  }
  .city {
  	width: 1.14rem;
  	line-height: .86rem;
  	text-align: center;
  }
  .swiper-img-con {
  	overflow: hidden;
    width: 100%;
    height: 0;
    padding-bottom: 31.25%;
  }
  .swiper-img {
  	width: 100%;
  }
  .icon-wrapper {
    position: relative;
  }
  .icon-item {
    box-sizing: border-box;
    float: left;
    width: 25%;
    padding-top: .3rem;
    text-align: center;
  }
  .icon-img-con {
    width:.66rem;
    height: .66rem;
    display: inline-block;
  }
  .icon-img {
    width: 100%;
  }
  .icon-title {
    box-sizing: border-box;
    font-size: 0.26rem;
    color: #1b1b1b;
    text-align: center;
    padding-top:0.21rem;
  }
  .icon-pagination {
    padding-top:0.2rem;
    text-align: center;
  }
  .icon-text {
    padding-top: .05rem;
    display: block;
    width: 100%;
    height: .6rem
  }
  .mp-listentrance-item{
    height: .49rem;
    width: 1.875rem;
  }
  .promotion-solid {
    display: block;
    width: 100%;
    height: .01rem;
    border-top: 0.01rem #e1e1e1 solid
  }
  .promotion-solid-vertical {
    display: block;
    width: .01rem;
    border-right: 0.01rem #e1e1e1 solid
  }
  .promotion-box {
    width: 100%;
    overflow: hidden
  }
  .promotion-box-con {
    position: relative;
    display: flex;
  }

  .promotion-item {
    width: 100%;
  }
  .geolocation {
    display: block;
    padding: .35rem 1.18rem;
    font-size: .25rem;
    margin: 0 auto;
    color: #000
  }
  .hot-spring {
    display: block;
    padding: .35rem 1.07rem;
    margin: 0 auto;
    font-size: .25rem;
    color: #000
  }
  .null-background {
    height: .2rem;
    width: 100%;
    background: #f5f5f5;
  }
  .discount {
    width: 100%
  }
  .discount-box {
    display: flex;
    width: 100%
  }
  .discount-water {
    width: 100%;
    background: url(http://img1.qunarzz.com/piao/fusion/1710/a2/e395615b16fb1302.png) center center no-repeat;
    background-size: auto 100%;
    padding: .7rem 0
  }
  .discount-tickies {
    width: 100%;
    background: url(http://img1.qunarzz.com/piao/fusion/1711/8a/4c62d1a89fc2d602.png) center center no-repeat;
    background-size: auto 100%;
    padding: .7rem 0
   }
   .sales-recommend h2{
    width: 100%;
    height: .8rem;
    padding-left: .26rem;
    line-height: .8rem;
    color: #212121;
   }
   .sales-recommend {
    background: #f5f5f5;
   }
   .hot-box {
    display: flex;
    flex-direction: column;
   }
   .page-bottom {
    width: 100%;
   }
   .hot-bottom {
    width: 100%
   }
   .hot-item-box {
    float: left;
    padding: .2rem;
   }
   .hot-img-con {
    width: .7rem;
    height: .7rem
   }

</style>
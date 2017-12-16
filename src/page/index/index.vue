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
        <swiper-slide>
          <div class="swiper-img-con">
            <img class="swiper-img" src="http://img1.qunarzz.com/piao/fusion/1710/f5/57137c621d75ba02.jpg_640x200_b984ddf7.jpg"/>
          </div>
        </swiper-slide>
        <div class="swiper-pagination"  slot="pagination"></div>
      </swiper>
      <div>123123</div>

	</div>
</template>
<script>
export default {

  name: 'Index',
  data () {
    return {
      swiperInfo: [],
      swiperOption: {
        loop: true,
        pagination: '.swiper-pagination',
        autoplay: 2000
      }
    }
  },

  created () {
    this.getIndexData()
  },
  methods: {

    getIndexData () {
      this.$http.get('./static/index.json')
        .then(this.handleGetDataSucc.bind(this))
    },

    handleGetDataSucc (res) {
      this.swiperInfo = res.body.data.swiper
    }
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
</style>
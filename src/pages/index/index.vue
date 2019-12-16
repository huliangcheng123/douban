<template>
  <div class="home">
    <div class="topBar">
      <div class="logo">豆瓣</div>
      <icon type="search" class="search" color="#00b600" size="23" />
      <div class="openApp">打开豆瓣App</div>
    </div>
    <div class="hotMovies">
      <div class="head">
        <div class="title">影院热映</div>
        <div class="morelink">更多</div>
      </div>
      <scroll-view scroll-x="true" style="height: 100%;">
        <div
          v-for="(item, index) in hotMoviesList"
          :key="index"
          class="scroll-view-item"
        >
          <div class="details">
            <img :src="item.images.large" alt="" class="binner" />
            <div class="movieName">{{item.title}}</div>
            <div class="rating" v-if="item.rating.average" >
              <div class="start">
                <img
                  src="../../../static/images/star.svg"
                  alt=""
                  v-for="(items, indexs) in 5"
                  :key="indexs"
                />
              </div>
              <span>{{item.rating.average}}</span>
            </div>
            <div v-else>暂无评论</div>
          </div>
        </div>
      </scroll-view>
    </div>
  </div>
</template>

<script>
// import {request} from '../../../request/index'
export default {
  data () {
    return {
      hotMoviesList: []
    }
  },
  created () {
    this.getTheaterMovies()
  },
  methods: {
    // 获取热门电影
    getTheaterMovies () {
      wx.request({
        url: 'https://api.douban.com/v2/movie/in_theaters?apikey=0df993c66c0c636e29ecbb5344252a4a',
        header: {
          'Content-Type': 'application/x-www-form-urlencoded'
        },
        method: 'GET',
        success: (result) => {
          console.log(result)
          this.hotMoviesList = result.data.subjects
        },
        fail: () => {},
        complete: () => {}
      })
    }
  }
}
</script>

<style lang="less">
.home {
  padding: 0 38rpx 0 38rpx;
  .topBar {
    border-bottom: 1px solid #ccc;
    display: flex;
    height: 94rpx;
    align-items: center;
    vertical-align: center;
    .logo {
      font-size: 55rpx;
      color: #00b600;
    }
    .search {
      margin-left: 28rpx;

      flex: 1;
    }
    .openApp {
      background-color: #00b600;
      width: 200rpx;
      height: 50rpx;
      border-radius: 8rpx;
      color: #fff;
      line-height: 50rpx;
      text-align: center;
      font-size: 28rpx;
    }
  }
  .head {
    height: 87rpx;
    display: flex;
    justify-content: space-between;
    align-items: center;
    .title {
      font-size: 31rpx;
      font: 700;
    }
    .morelink {
      color: #00b600;
    }
  }
  scroll-view {
    white-space: nowrap;
    margin-top: 12px;
    .scroll-view-item {
      margin-right: 13px;
      display: inline-block;
      width: 200rpx;

      .binner {
        width: 200rpx;
        height: 286rpx;
      }
      .movieName {
        width: 100%;
        overflow: hidden;
        white-space: nowrap;
        text-overflow: ellipsis;
      }
      .rating {
        display: flex;

        img {
          width: 20rpx;
          height: 20rpx;
        }
      }
    }
  }
}
</style>

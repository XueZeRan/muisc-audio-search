<template>
  <div class="container">
    <div class="jumbotron">
      <div class="text-center">
        <h1 class="display-3">iTunes Search API</h1>
      </div>
      <p class="lead">audio~~Search ~~API允许您在网站中放置搜索字段，搜索电影相关视频资料~~~~~~</p>
      <hr class="my-4">
      <div class="text-center">
        <form id="search-form">
          <div class="form-group">
            <input ref="searchvalue" type="text" id="search-text" class="form-control" placeholder="输入电影名·关键字·相关字词搜索...例如：美國隊長">
          </div>
          <button @click="searchadiou" type="submit" class="btn btn-primary btn-block">搜索</button>
        </form>
      </div>
    </div>
    <div class="jumbotron" v-for="(item,index) of music" :key="index">
      <h2>{{item.trackCensoredName}}·类型：{{item.primaryGenreName}}</h2>
      <div class="audio">
        <video width="100%" controls>
          <source :src="item.previewUrl" type="video/x-m4v">
        </video>
        <div @click="off(index)" class="vjs-poster" tabindex="-1" aria-disabled="flase" style="background-image: url(https://static.anime1.me/playerImg/8.jpg);position: absolute"></div>
      </div>
      <p class="lead">{{item.longDescription}}</p>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
 name:'au',
  props: {
    
  },
  data() {
    return {
      searchvalue:null,
      music:null,
      oppo:true,
      // nunberindex:null
    }
  },
  methods: {
    getHomeInfo() {
      axios.get(`https://itunes.apple.com/search?term=${this.searchvalue}&country=TW&limit=26&media=movie`)
      .then(this.getHomeInfoSucc)
    },
    getHomeInfoSucc(res) {
      res=res.data.results
      // for(let i =0;i<res.length;i++){
      //   const ms = res[i]
      //   console.log(ms.kind)
      //   // if(ms.kind !== 'song'){
      //   //   continue
      //   // }
      //   // console.log(ms.kind)
      // }
      this.music=res
      // console.log(res)
      // console.log(res.length)
      if(this.music.length == 0){
        alert('找不到相关视频,请输入正确信息')
      }
      // console.log(this.music)
      // console.log(this.music[0].collectionName)
      // console.log(this.music[0].primaryGenreName)
      // console.log(this.music[0].previewUrl)
      // console.log(this.music[0].longDescription)
    },
    searchadiou(e) {
      e.preventDefault() //阻止默认事件
      this.searchvalue =this.$refs.searchvalue.value
      // console.log(this.searchvalue)
      this.getHomeInfo()
    },
    off(index){
      // console.log(index)
      // this.nunberindex=index
      document.getElementsByClassName('vjs-poster')[index].style.position=''
    }
  }
}
</script>

<style lang='stylus' scoped>
  .audio
    position relative
    width 1000px
    // height 563px
    @media screen and (max-width: 1200px)
      width 866px
      // width 563px
    @media screen and (max-width: 991px)
      width 626px
      // width 563px
    @media screen and (max-width: 767px)
      width 446px
      // width 563px
    @media screen and (max-width: 575px)
      width 100%
      // width 563px
    .vjs-poster
      // display: inline-block
      vertical-align: middle
      background-repeat: no-repeat
      background-position: 50% 50%
      background-size: contain
      background-color: #000
      cursor: pointer
      margin: 0
      padding: 0
      // position: absolute
      top: 0
      right: 0
      bottom: 0
      left: 0
      height: 100%
</style>
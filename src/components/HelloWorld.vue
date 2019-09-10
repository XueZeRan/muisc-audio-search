<template>
  <div class="hello">
    <div class="container">
      <div class="jumbotron">
        <div class="text-center">
          <h1 class="display-3">iTunes Search API</h1>
        </div>
        <p class="lead">搜索音乐~~Search API允许您在网站中放置搜索字段，以搜索iTunes Store和Apple Books Store中的内容。您可以搜索各种内容; 包括书籍，电影，播客，音乐，音乐视频，有声读物和电视节目</p>
        <hr class="my-4">
        <div class="text-center">
          <form id="search-form">
            <div class="form-group">
              <input ref="searchvalue" type="text" id="search-text" class="form-control" placeholder="输入歌曲名...搜索歌曲,作者~~例如：周杰伦">
            </div>
            <button @click="searchmusic" type="submit" class="btn btn-primary btn-block">搜索</button>
          </form>
        </div>
      </div>
      <div class="card-columns">
        <div class="card" v-for="(item,index) of music" :key="index" v-if="item.kind =='song'">
          <img :src="item.artworkUrl100" class="card-img-top">
          <div class="card-body">
            <h5 class="card-title">{{item.trackName}}</h5>
            <p class="card-text">{{item.artistName}}</p>
          </div>
          <ul class="list-group list-group-flush">
            <li class="list-group-item">{{item.collectionName}}</li>
            <li class="list-group-item">{{item.primaryGenreName}}·{{item.releaseDate.split('-',1)}}</li>
            <li class="list-group-item">
              试听:<br/>
              <audio class="audiomusic" :src="item.previewUrl" controls='controls'></audio>
            </li>
          </ul>
          <div class="card-body">
            <a :href="item.trackViewUrl" target="_blank" class="card-link">show in apple music</a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'HelloWorld',
  props: {
    
  },
  data() {
    return {
      searchvalue:null,
      music:null
    }
  },
  methods: {
    getHomeInfo() {
      axios.get(`https://itunes.apple.com/search?term=${this.searchvalue}&country=TW&limit=25`)
      .then(this.getHomeInfoSucc)
    },
    getHomeInfoSucc(res) {
      res=res.data.results
      // for(let i =0;i<res.length;i++){
      //   const ms = res[i]
      //   // console.log(ms.kind)
      //   if(ms.kind !== 'song'){
      //     continue
      //   }
      //   // console.log(ms.kind)
      // }
      this.music=res
      if(this.music.length == 0){
        alert('找不到相关音乐,请输入正确信息')
      }
      // console.log(res.kind)
      // console.log(res.length)
      // console.log(this.music)
    },
    searchmusic(e) {
      e.preventDefault() //阻止默认事件
      this.searchvalue =this.$refs.searchvalue.value
      // console.log(this.searchvalue)
      this.getHomeInfo()
    }
  },
  created() {
    // this.getHomeInfo()  //让页面挂载好后执行该函数
  },
  mounted() {
    
  },
  updated() {
    
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang='stylus' scoped>
  .audiomusic
    width 100%
    // background blue
</style>

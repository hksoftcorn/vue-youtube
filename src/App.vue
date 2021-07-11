<template>
  <div id="app">
    <h1>Vue-Youtube Porject</h1>
    <header>
      <SearchBar
        @input-search="onInputSearch"
      />
    </header>
    <section>
      <VideoDetail 
        :video="selectVideo"
      />
      <VideoList
        :videos="videos"
        @select-video="onSelectVideo"
      />
    </section>
  </div>
</template>

<script>
import axios from 'axios'
import SearchBar from "@/components/SearchBar.vue";
import VideoList from "@/components/VideoList.vue";
import VideoDetail from "@/components/VideoDetail.vue";


const API_KEY = process.env.VUE_APP_YOUBUE_API_KEY
const API_URL = 'https://www.googleapis.com/youtube/v3/search'

export default {
  name: "App",
  components: {
    SearchBar,
    VideoList,
    VideoDetail,
  },

  data: function () {
    return {
      searchData: '',
      videos: [],
      selectVideo: '',
    }
  },
  methods: {
    // VideoListItem에서 emit으로 올라온 "선택된 비디오" 정보입니다.
    onSelectVideo: function (video) {
      this.selectVideo = video
    },

    // Youtube Api를 통한 검색 결과 반환
    onInputSearch: function (searchData) {
      this.searchData = searchData

      const params = {
        key: API_KEY,
        part: 'snippet',
        type: 'video',
        q: this.searchData,
      }
      axios({
        url: API_URL,
        methods: 'get',
        params
      })
        .then(response => {
          this.videos = response.data.items
        })
        .catch(error => {
          console.log(error)
        })
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  padding-left: 1rem;
  padding-right: 1rem;
}

section,
header {
  width: 80%;
  margin: 0 auto;
  padding: 1rem 0;
}

section {
  display: flex;
}
</style>
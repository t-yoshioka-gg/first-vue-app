<template>
  <div>
    <button @click="clearResults">Clear the results</button>
    <SearchBar @termChange="onTermChange"></SearchBar>
    <VideoList :videos="videos" @removeVideo="removeVideo"></VideoList>
    {{videos.length}}
  </div>
</template>

<script>
import SearchBar from './components/SearchBar.vue';
import VideoList from "./components/VideoList.vue";

import axios from "axios";

const API_KEY = "AIzaSyDO53vAiymIWITBifmeVWlTd5Z5598HqWo";


export default {
  name: "App",
  components: {
    SearchBar,
    VideoList
  },
  data() {
    return {
      videos: []
    }
  },
  methods: {
    async onTermChange (searchTerm) {
      const req = await axios.get("https://www.googleapis.com/youtube/v3/search", {
        params: {
          key: API_KEY,
          type: "video",
          part: "snippet",
          q: searchTerm
        }
      })
      const res = await req.data;
      this.videos = res.items;
    },
    clearResults(e) {
      e.preventDefault();
      this.videos = [];
    },
    removeVideo(seletededVideo) {
      this.videos = this.videos.filter(video => {
          console.log(video);
          return video.snippet.title !== seletededVideo.snippet.title;
      })
    }
  },
  watch: {
     videos(valueAfterUpdate, valueBeforeUpdate) {
       console.log(valueAfterUpdate, valueBeforeUpdate);
    }
  }
};
</script>

<style>

</style>

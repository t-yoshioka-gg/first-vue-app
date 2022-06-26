<template>
<div>
  <ul>
    <VideoListItem 
    :key="video.etag" 
    v-for="video in videos"
    :video="video"
    @removeVideo="removeVideo"
    ></VideoListItem>
  </ul>
  <p>{{text}}</p>
</div>
</template>

<script>
import VideoListItem from './VideoListItem.vue';
export default {
  components: { VideoListItem},
  name: "VideoList",
   data: function() {
    return {
      text: "hola"
    }
  },
  props: {
    videos: Array
  },
  methods: {
    removeVideo(video) {
      this.$emit("removeVideo", video);
    }
  },
  computed: {
    videosToList() {
      return this.videos.length;
    }
  },
  
}
</script>

<style>

</style>
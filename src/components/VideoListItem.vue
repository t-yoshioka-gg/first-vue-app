<template>
  <li @click="clickHander">
    {{video.snippet.title}}
  </li>
</template>

<script>
export default {
  name: "VideoListItem",
  props: {
    video: Object
  },
  methods: {
    clickHander() {
      this.$emit("removeVideo", this.video);
    }
  }
}
</script>

<style>

</style>
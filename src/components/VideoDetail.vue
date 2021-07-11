<template>
  <div v-if="video" class="video-detail">
    <div class="video-container">
      <iframe :src="videoUrl" frameborder="0"></iframe>
    </div>
    <h2>{{ stringUnescape(video.snippet.title) }}</h2>
    <p>{{ stringUnescape(video.snippet.description) }}</p>
  </div>
</template>

<script>
import _ from 'lodash'

export default {
  name: 'VideoDetail',
  props: {
    video: {
      type: [String, Object],
    }
  },
  computed: {
    videoUrl: function () {
      const videoId = this.video.id.videoId
      return `https://www.youtube.com/embed/${videoId}`
    },
    stringUnescape() {
      return (rawText) => {
        return _.unescape(rawText)
      }
    }
  }
}
</script>

<style>
.video-detail {
  width: 70%;
  padding-right: 1rem;
}

.video-container {
  position: relative;
  padding-top: 56.25%;
}

.video-container > iframe {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}
</style>
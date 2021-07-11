<template>
  <li @click="selectVideo" class="list-group-item">
    <img :src="youtubeImgSrc" alt="#">
    {{ stringUnescape(video.snippet.title) }}
  </li>
</template>

<script>
import _ from 'lodash'

export default {
  name: 'VideoListItem',
  props: {
    video: {
      type: Object,
    }
  },
  methods: {
    selectVideo: function () {
      this.$emit('select-video', this.video)
    }
  },
  computed: {
    youtubeImgSrc: function () {
      return this.video.snippet.thumbnails.default.url
    },
    stringUnescape() {
      return (rawText) => {
        return _.unescape(rawText)
      }
    }
  },
  // Disallow using deprecated filters syntax (in Vue.js 3.0.0+)
  // filters: {
  //   stringUnescape: function (rawText) {
  //     return _.unescape(rawText)
  //   }
  // },
}
</script>

<style>
.list-group .list-group-item {
  display: flex;
  margin-bottom: 1rem;
  cursor: pointer;
}

.list-group .list-group-item:hover {
  background: #eee;
}

.list-group .list-group-item img {
  height: fit-content;
  margin-right: 0.5rem;
}

</style>
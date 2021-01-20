<template>
  <div class="video-container">
    <ali-player
      ref="player"
      :autoplay="false"
      :is-live="true"
      :playsinline="true"
      width="100%"
      height="500px"
      :use-h5prism="true"
      :use-flash-prism="false"
      :source="url"
      :cover="coverimage"
    />
    <button @click="play">播放</button>
    <button @click="pause">暂停</button>
  </div>
</template>

<script>
import VueAliplayer from 'vue-aliplayer'
export default {
  name: 'Aliplayer',
  components: {
    'ali-player': VueAliplayer
  },
  data() {
    return {
      // url: "rtmp://58.200.131.2:1935/livetv/hunantv", //湖南卫视
      // url: "rtmp://mobliestream.c3tv.com:554/live/goodtv.sdp", //韩国GoodTV
      // url: "http://static.smartisanos.cn/common/video/t1-ui.mp4",
      url:
        'https://vodcdn.alicdn.com/oss/taobao-ugc/e6fb60eae8594f9e812233489bfa2732/1476578718/video.mp4',
      coverimage: require('../../assets/AliPlayerHome.png')
    }
  },
  methods: {
    play: function() {
      const player = this.$refs.player.instance
      player && player.play()
    },
    pause: function() {
      const player = this.$refs.player.instance
      player && player.pause()
    }
  }
}
</script>

<style scoped>
.video-container {
  display: block;
  width: 80%;
  height: 100%;
  margin-left: auto;
  margin-right: auto;
  margin-bottom: auto;
}
</style>


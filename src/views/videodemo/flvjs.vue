<template>
  <div class="video-container">
    <div>
      <video ref="player" class="centeredVideo" name="videoElement" controls autoplay />
    </div>
  </div>
</template>
<script>
import flvjs from 'flv.js'
export default {
  data() {
    return {
      flvPlayer: null
    }
  },
  mounted() {
    if (flvjs.isSupported()) {
      const video = this.$refs.player
      if (video) {
        this.flvPlayer = flvjs.createPlayer({
          type: 'flv',
          // isLive: true,
          url: 'https://mister-ben.github.io/videojs-flvjs/bbb.flv' // 网络动画视频
        })
        this.flvPlayer.attachMediaElement(video)
        try {
          this.flvPlayer.load()
          this.flvPlayer.play()
        } catch (error) {
          console.log(error)
        }
      }
    }
  }
}
</script>
<style>
.centeredVideo {
  display: block;
  width: 80%;
  height: 60%;
  margin-left: auto;
  margin-right: auto;
  margin-bottom: auto;
}
.video-container {
  display: block;
  width: 80%;
  height: 100%;
  margin-left: auto;
  margin-right: auto;
  margin-bottom: auto;
}
</style>

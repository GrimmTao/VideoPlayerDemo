<template>
  <div>
    <LivePlayer id="video" :video-url="url" :poster="image" :autoplay="false" :live="false" />
  </div>
</template>

<script>
import LivePlayer from '@liveqing/liveplayer'
export default {
  components: {
    LivePlayer
  },
  data() {
    return {
      image: require('../../assets/LivePlayerHome.png'), // 封面图片
      url:
        'https://vodcdn.alicdn.com/oss/taobao-ugc/1dde6e764244406cbe5962b26eee078c/1476754829/video.mp4' // 网络MP4文件
      // url: "rtmp://58.200.131.2:1935/livetv/hunantv" //湖南卫视
      // url: "rtmp://mobliestream.c3tv.com:554/live/goodtv.sdp" //韩国GoodTV
      // url: "http://10.40.101.112:10080/hls/live/live_live.m3u8" //HLS(m3u8)源地址
    }
  }
}
</script>

<style scoped>
#video {
  width: 800px;
  height: 600px;
  margin: 0px auto;
}
</style>


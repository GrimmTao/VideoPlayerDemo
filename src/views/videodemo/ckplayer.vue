<template>
  <div class="video-container">
    <div id="videoElement" class="demo-video" />
  </div>
</template>
<script>
export default {
  data() {
    return {}
  },
  mounted() {
    var videoObject = {
      container: 'demo-video', // 容器的ID或className
      variable: 'player', // 播放函数名称
      live: true,
      flashplayer: true, // 如果强制使用flashplayer则设置成true
      autoplay: false, // 是否自动播放
      poster: require('../../assets/CkplayerHome.png'), // 封面图片
      video: 'rtmp://58.200.131.2:1935/livetv/hunantv' // 湖南卫视
    }
    // 定义一个对象
    var player = new ckplayer(videoObject)
  }
}
</script>
<style>
.demo-video {
  width: 100%;
  height: 600px;
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

<template>
  <div class="video-container">
    <video-player
      ref="videoPlayer"
      class="video-player vjs-custom-skin"
      :playsinline="true"
      :options="playerOptions"
    />
  </div>
</template>

<script>
export default {
  data() {
    return {
      playerOptions: {
        // 播放速度
        playbackRates: [1.0, 1.5, 2.0],
        // 如果true,浏览器准备好时开始回放。
        autoplay: false,
        // 默认情况下将会消除任何音频。
        muted: false,
        // 导致视频一结束就重新开始。
        loop: false,
        // 建议浏览器在<video>加载元素后是否应该开始下载视频数据。auto浏览器选择最佳行为,立即开始加载视频（如果浏览器支持）
        preload: 'auto',
        language: 'zh-CN',
        // 将播放器置于流畅模式，并在计算播放器的动态大小时使用该值。值应该代表一个比例 - 用冒号分隔的两个数字（例如"16:9"或"4:3"）
        aspectRatio: '16:9',
        // 当true时，Video.js player将拥有流体大小。换句话说，它将按比例缩放以适应其容器。
        fluid: true,
        sources: [
          {
            // type: "rtmp/flv", //类型
            type: 'rtmp/mp4', // 类型
            // src: "rtmp://mobliestream.c3tv.com:554/live/goodtv.sdp" //韩国GoodTV
            src: 'rtmp://58.200.131.2:1935/livetv/hunantv' // 湖南卫视
          }
        ],
        techOrder: ['flash'],
        controls: true,
        // 你的封面地址
        poster: require('../../assets/VueVideoHome.jpg'),
        // 允许覆盖Video.js无法播放媒体源时显示的默认信息。
        notSupportedMessage: '此视频暂无法播放，请稍后再试',
        controlBar: {
          timeDivider: false,
          durationDisplay: false,
          remainingTimeDisplay: false,
          // 全屏按钮
          fullscreenToggle: true
        }
      }
    }
  }
}
</script>

<style scoped>
.video-container {
  display: block;
  width: 50%;
  height: 50%;
  margin-left: auto;
  margin-right: auto;
  margin-bottom: auto;
}
</style>


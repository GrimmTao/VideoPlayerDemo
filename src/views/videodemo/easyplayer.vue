<template>
  <div class="easyplayer">
    <div id="Player" />
  </div>
</template>

<script>

export default {
  data() {
    return {
      player: '',
      url: 'http://10.40.2.21:10080/hls/HaIDX5fGR/HaIDX5fGR_live.m3u8'
    }
  },
  mounted() {
    // 实例化播放器
    this.player = new WasmPlayer(null, 'Player', this.callbackfun)
    // 设置封面照片(未生效)
    this.player.setSnap('../../assets/AliPlayerHome.png')
    // 调用播放
    this.player.play(this.url, 0)
  },
  methods: {
    callbackfun(e) {
      console.log('callbackfun', e)
    }
  }
}
</script>
<style>
  .easyplayer {
  width: 800px;
  height: 600px;
  margin: 0px auto;
}
</style>

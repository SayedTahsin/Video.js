<template>
  <div>
    <video ref="videoPlayer" class="video-js vjs-default-skin" controls preload="auto">
    </video>
  </div>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue';
import videojs from 'video.js';
import 'video.js/dist/video-js.css';

const videoPlayer = ref(null);
let player = null;

onMounted(() => {
  player = videojs(videoPlayer.value, {
    autoplay: false,
    controls: true,
    loop: false,
    preload: 'auto',
    playbackRates: [0.5, 1, 1.5, 2],
    volume: 0.5,
    sources: [{
      src: 'https://bitdash-a.akamaihd.net/content/sintel/hls/playlist.m3u8',
      type: 'application/x-mpegURL',
    }]
  });

});

onBeforeUnmount(() => {
  if (player) {
    player.dispose();
  }
});
</script>

<style scoped>
.video-js {
  width: 100%;
  height: 500px;
}
</style>

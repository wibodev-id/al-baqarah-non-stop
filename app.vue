<template>
  <div class="video-container">
    <iframe
      id="yt-player"
      :src="`https://www.youtube.com/embed/${videoId}?autoplay=1&mute=1&loop=1&playlist=${videoId}&controls=0&showinfo=0&rel=0&modestbranding=1&playsinline=1&enablejsapi=1`"
      frameborder="0"
      allow="autoplay; fullscreen"
      allowfullscreen
    ></iframe>
    <div v-if="muted" class="overlay" @click="unmute">
      <div class="tap-hint">tap untuk nyalakan suara</div>
    </div>
    <div v-else class="overlay"></div>
  </div>
</template>

<script setup>
const videoId = 'lisrO0muALo'
const muted = ref(true)
let player = null

onMounted(() => {
  const tag = document.createElement('script')
  tag.src = 'https://www.youtube.com/iframe_api'
  document.head.appendChild(tag)

  window.onYouTubeIframeAPIReady = () => {
    player = new window.YT.Player('yt-player', {
      events: {
        onReady: (e) => {
          e.target.mute()
          e.target.playVideo()
        },
      },
    })
  }
})

function unmute() {
  if (player && player.unMute) {
    player.unMute()
    player.setVolume(100)
    player.playVideo()
    muted.value = false
  }
}
</script>

<style>
body, html {
  margin: 0;
  padding: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
  background-color: #000;
}

.video-container {
  position: relative;
  width: 100vw;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

iframe {
  width: 100vw;
  height: 100vh;
  pointer-events: none;
}

.overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 10;
  pointer-events: auto;
  background: transparent;
  display: flex;
  justify-content: center;
  align-items: flex-end;
  padding-bottom: 40px;
  box-sizing: border-box;
  cursor: pointer;
}

.tap-hint {
  color: #fff;
  background: rgba(0, 0, 0, 0.6);
  padding: 10px 20px;
  border-radius: 999px;
  font-family: system-ui, sans-serif;
  font-size: 14px;
  animation: pulse 2s ease-in-out infinite;
}

@keyframes pulse {
  0%, 100% { opacity: 0.7; }
  50% { opacity: 1; }
}
</style>

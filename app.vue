<template>
  <div class="video-container">
    <iframe 
      src="https://www.youtube.com/embed/lisrO0muALo?autoplay=1&mute=0&loop=1&playlist=lisrO0muALo&controls=0&showinfo=0&rel=0&modestbranding=1" 
      frameborder="0" 
      allow="autoplay; fullscreen" 
      allowfullscreen
    ></iframe>
    <!-- overlay layer to catch clicks and prevent interaction with the video -->
    <div class="overlay"></div>
  </div>
</template>

<style>
body, html {
  margin: 0;
  padding: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
  background-color: #000; /* Black background to prevent white flashes */
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
  /* Add scale if you want it to behave like object-fit: cover and hide black bars */
  /* transform: scale(1.3); */
  pointer-events: none; /* Disables mouse events on the iframe */
}

.overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 10;
  /* Catch all pointer events, effectively disabling the page */
  pointer-events: auto; 
  background: transparent;
}
</style>

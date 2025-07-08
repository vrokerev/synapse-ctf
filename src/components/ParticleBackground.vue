<template>
  <vue-particles id="tsparticles" :options="options" />
</template>

<script setup>
const options = {
  background: {
    color: {value: '#000000'}
  },
  fpsLimit: 90,
  interactivity: {
    events: {
      onHover: {enable: true, mode: 'grab'},
      resize: true
    },
    modes: {
      grab: {
        distance: 140,
        links: {opacity: 1}
      }
    }
  },
  particles: {
    color: {value: '#39ff14'},
    links: {
      color: '#39ff14',
      distance: 150,
      enable: true,
      opacity: 0.5,
      width: 1
    },
    move: {
      enable: true,
      speed: 1,
      direction: 'none',
      random: false,
      straight: false,
      outModes: 'out'
    },
    number: {
      value: 60,
      density: {
        enable: true,
        area: 800
      }
    },
    opacity: {value: 0.5},
    shape: {type: 'circle'},
    size: {value: 3}
  },
  detectRetina: true
}
</script>

<style scoped>
#tsparticles {
  position: fixed;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  z-index: 0;
  pointer-events: none;
}
</style>

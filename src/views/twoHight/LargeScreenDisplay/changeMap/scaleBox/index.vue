<template>
  <div
    ref="ScaleBox"
    class="ScaleBox"
    :style="{
      width: width + 'px',
      height: height + 'px',
    }"
  >
    <slot />
  </div>
</template>
<script>
export default {
  name: 'ScaleBox',
  props: {

  },
  data() {
    return {
      scale: '',
      width: 1920,
      height: 1080
    }
  },
  mounted() {
    this.setScale()
    window.addEventListener('resize', this.debounce(this.setScale, 100))
  },
  methods: {
    getScale() {
      const { width, height } = this
      const wh = window.innerHeight / height
      const ww = window.innerWidth / width
      // console.log(ww < wh ? ww : wh)
      return ww < wh ? ww : wh
    },
    setScale() {
      if (window.innerHeight === 1080) {
        this.height = 1080
      } else {
        this.height = 1080
      }
      this.scale = this.getScale()
      if (this.$refs.ScaleBox) {
        this.$refs.ScaleBox.style.setProperty('--scale', this.scale)
      }
    },
    debounce(fn, delay) {
      const delays = delay || 500
      let timer
      return function() {
        const th = this
        const args = arguments
        if (timer) {
          clearTimeout(timer)
        }
        timer = setTimeout(function() {
          timer = null
          fn.apply(th, args)
        }, delays)
      }
    }
  }
}
</script>

<style lang="scss">
#ScaleBox {
  --scale: 1;
}
.ScaleBox {
  position: absolute;
  transform: scale(var(--scale)) translate(-50%, -50%);
  display: flex;
  flex-direction: column;
  transform-origin: 0 0;
  left: 50%;
  top: 50%;
  transition: 0.3s;
  z-index: 999;
}
</style>

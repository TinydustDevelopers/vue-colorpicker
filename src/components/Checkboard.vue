<template>
  <div class="grid"
       :style="gridStyle"
       v-el:grid></div>
</template>

<script>
let _checkboardCache = {}

function renderCheckboard(c1, c2, size) {
  if (typeof document === 'undefined') return null
  let canvas = document.createElement('canvas')
  canvas.width = canvas.height = size * 2
  let ctx = canvas.getContext('2d')
  if (!ctx) return null
  ctx.fillStyle = c1
  ctx.fillRect(0, 0, canvas.width, canvas.height)
  ctx.fillStyle = c2
  ctx.fillRect(0, 0, size, size)
  ctx.translate(size, size)
  ctx.fillRect(0, 0, size, size)
  return canvas.toDataURL()
}

function getCheckboard(c1, c2, size) {
  let key = `${c1},${c2},${size}`

  if (_checkboardCache[key]) {
    return _checkboardCache[key]
  } else {
    let checkboard = renderCheckboard(c1, c2, size)
    _checkboardCache[key] = checkboard
    return checkboard
  }
}

export default {
  data() {
    return {
      size: 8,
      white: '#fff',
      grey: '#e6e6e6'
    }
  },
  computed: {
    // put in data or computed?
    gridStyle() {
      let background = getCheckboard(this.white, this.grey, this.size)
      return {
        background: `url(${background}) center left`
      }
    }
  }
}
</script>

<style scoped>
.grid {
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
}
</style>

<template>
    <div class="picker">
      <div class="saturation-container">
        <saturation :color="color" @color-change="handleColorChange"></saturation>
      </div>
      <div class="controls">
        <div class="sliders">
          <div class="hue-container">
            <hue :color="color" @color-change="handleColorChange"></hue>
          </div>
          <div class="alpha-container">
            <alpha
            :color="color"
            @color-change="handleColorChange"
            ></alpha>
          </div>
        </div>
        <div class="color-container">
          <div class="activeColor" :style="activeColorStyle"></div>
          <checkboard></checkboard>
        </div>
      </div>
      <editable
      :color="color"
      @color-change="handleColorChange"
      ></editable>
    </div>
</template>

<script>
import Hue from './components/Hue.vue'
import Alpha from './components/Alpha.vue'
import Saturation from './components/Saturation.vue'
import Checkboard from './components/Checkboard.vue'
import Editable from './components/Editable.vue'

export default {
  data() {
    return {
      color: {
        a: 1,
        h: 0,
        s: 0,
        v: 0,
        r: 0,
        g: 0,
        b: 0,
        hex: '#000000'
      }
    }
  },
  computed: {
    // TODO: fix
    activeColorStyle () {
      return {
        background: `rgba(${this.color.r},${this.color.g},${this.color.b},${this.color.a})`
      }
    }
  },

  components: {
    Hue, Alpha, Saturation, Checkboard, Editable
  },

  methods: {
    handleColorChange(colors) {
      console.log(colors)
      this.color.h = colors.hsva.h
      this.color.s = colors.hsva.s
      this.color.v = colors.hsva.v
      this.color.a = colors.hsva.a
      this.color.r = colors.rgba.r
      this.color.g = colors.rgba.g
      this.color.b = colors.rgba.b
      this.color.hex = colors.hex
      this.$dispatch('child-color-change', this.color)
    }
  }
}
</script>

<style>
#app {
  position: relative;
}
.picker {
  width: 200px;
  padding: 10px 10px 0;
  box-sizing: initial;
  background: #fff;
  border-radius: 4px;
  box-shadow: 0 0 0 1px rgba(0,0,0,.15), 0 8px 16px rgba(0,0,0,.15);
}
.saturation-container {
  width: 100%;
  padding-bottom: 75%;
  position: relative;
  overflow: hidden;
}

.controls {
  display: flex;
}

.sliders {
  padding: 4px 0;
  flex: 1;
}

.color-container {
  width: 24px;
  height: 24px;
  position: relative;
  margin-top: 5px;
  margin-left: 5px;
  border-radius: 3px;
}

.activeColor {
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  border-radius: 2px;
  box-shadow: inset 0 0 0 1px rgba(0,0,0,.15), inset 0 0 4px rgba(0,0,0,.25);
  z-index: 2;
}

.hue-container {
  position: relative;
  height: 10px;
  overflow: hidden;
}

.activeColor {
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  border-radius: 2px;
  box-shadow: inset 0 0 0 1px rgba(0,0,0,.15), inset 0 0 4px rgba(0,0,0,.25);
  z-index: 2;
}

.alpha-container {
  position: relative;
  height: 10px;
  margin-top: 4px;
  overflow: hidden;
}
</style>

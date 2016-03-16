<template>
  <h1>computer demo</h1>
  <button @click="add">add</button>
  <h2>x y</h2>
  <div v-for="a in arr">
    <span>x: {{a}}</span>
  </div>
  <div v-for="item in foo">
    <span>{{item.x}} {{item.y}}</span>
  </div>
</template>

<script>
export default {
  data () {
    return {
      arr: [0]
    }
  },

  computed: {
    foo () {
      return this.arr.map(x => ({x: x, y: 0}))
    }
  },

  methods: {
    add () {
      let n = this.arr[0] + this.arr.length
      this.arr.push(n)
    }
  }
}
</script>

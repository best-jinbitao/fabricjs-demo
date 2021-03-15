<template>
  <div class="hello">
    <canvas id="canvas" class="ctx"></canvas>
  </div>
</template>

<script>
import { fabric } from 'fabric'
export default {
  name: "HelloFabric",
  props: {
    msg: String
  },
  data() {
    return {
      canvas: null
    }
  },
  mounted() {
    this.$nextTick(() => {
      window.addEventListener('resize', () => { //监听浏览器窗口大小改变
      });
    })
    this.init()

  },
  methods: {
    init() {
      this.canvas = new fabric.Canvas('canvas', {
        width: 1900, height: 920,

      });

      const longer = window.innerWidth > window.innerHeight ? window.innerWidth : window.innerHeight
      let vLine
      let hLine
      let distance = 10
      for (let i = 1; i * distance < longer; i++) {
        const lineDef = {
          fill: 'black',
          stroke: 'rgba(0, 0, 0, 0.1)',
          strokeWidth: 1,
          selectable: false
        }
        // draw vLine
        vLine = new fabric.Line([i * distance, 0, i * distance, this.canvas.height], lineDef)
        // draw hLine
        hLine = new fabric.Line([0, i * distance, this.canvas.width, i * distance], lineDef)
        this.canvas.add(vLine, hLine)
      }
    }
  }
};
</script>

<style scoped>
.ctx {
  width: 5000px;
  height: 5000px;
  border: 1px solid black;
}
</style>

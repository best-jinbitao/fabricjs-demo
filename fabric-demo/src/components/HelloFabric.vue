<template>
  <div style="width:100%">
    <div class="palette" style="">调色板</div>
    <div class="my-canvas">
      <canvas id="canvas" class="ctx"></canvas>
    </div>
    <div class="instructions">
      <span>
        在线画图实现
      </span>
    </div>
  </div>
</template>

<script>
import { fabric } from "fabric";
export default {
  name: "HelloFabric",
  props: {
    msg: String
  },
  data() {
    return {
      canvas: null
    };
  },
  mounted() {
    this.$nextTick(() => {
      window.addEventListener("resize", () => {
        //监听浏览器窗口大小改变
      });
    });
    this.init();
  },
  methods: {
    init() {
      this.canvas = new fabric.Canvas("canvas", {
        width: 1000,
        height: 600
      });
      // this.canvas.defaultCursor = "move";
      // this.canvas.hoverCursor = "pointer";

      const longer =
        window.innerWidth > window.innerHeight
          ? window.innerWidth
          : window.innerHeight;
      let vLine;
      let hLine;
      let distance = 10;
      for (let i = 1; i * distance < longer; i++) {
        const lineDef = {
          fill: "black",
          stroke: "rgba(0, 0, 0, 0.1)",
          strokeWidth: 1,
          selectable: false,
          hoverCursor: "default"
        };
        // draw vLine
        vLine = new fabric.Line(
          [i * distance, 0, i * distance, this.canvas.height],
          lineDef
        );
        // draw hLine
        hLine = new fabric.Line(
          [0, i * distance, this.canvas.width, i * distance],
          lineDef
        );
        this.canvas.add(vLine, hLine);
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
.palette {
  width: 998px;
  height: 100px;
  margin: 5px auto;
  border: 1px solid;
}
.my-canvas {
  text-align: center;
  margin: 30px auto;
  width: 1000px;
  height: 600px;
}
.instructions {
  font-size: 12px;
  background: rgb(196, 229, 241);
  width: 998px;
  height: 100px;
  margin: 5px auto;
  border: 1px solid;
}
</style>

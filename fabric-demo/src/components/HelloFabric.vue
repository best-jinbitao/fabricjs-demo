<template>
  <div style="width:100%">
    <div class="palette">
      <button type="button" class="button">画笔</button>
      <button type="button" class="button">直线</button>
      <button type="button" class="button">折线</button>
      <button type="button" class="button">矩形</button>
      <button type="button" class="button">三角形</button>
      <button type="button" class="button">圆形</button>
      <button type="button" class="button">椭圆</button>
      <button type="button" class="button">更多图形</button>
      <button type="button" class="button">文本</button>
      <button type="button" class="button">放大</button>
      <button type="button" class="button">缩小</button>
      <button type="button" class="button">填充颜色</button>
      <button type="button" class="button">形状填充</button>
      <button type="button" class="button">轮廓颜色</button>
      <button type="button" class="button">轮廓填充</button>
      <button type="button" class="button">形状填充</button>
      <button type="button" class="button">轮廓填充</button>
    </div>
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
    // this.drawLine();
  },
  methods: {
    init() {
      this.canvas = new fabric.Canvas("canvas", {
        width: 1000,
        height: 600
      });
    },
    drawLine() {
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
.button {
  width: 48px;
  height: 48px;
  background: white;
  border: 1px solid rgb(173, 175, 177);
  margin: 1px;
  border-radius: 8px;
  outline: none;
}
.button:focus {
  border: 2px solid rgb(83, 135, 187);
}

.ctx {
  width: 5000px;
  height: 5000px;
  border: 1px solid black;
}
.palette {
  display: flex;
  flex-wrap: wrap;
  width: 998px;
  height: 100px;
  margin: 5px auto;
  border: 1px solid #9e9fa0;
  background: rgb(229, 228, 226);
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

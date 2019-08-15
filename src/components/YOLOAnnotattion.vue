<template>
  <div id="image-annotation">
    <canvas ref="canvas" width="640" height="480"></canvas>
    <Rectangles v-bind:rectangles="rects" v-on:check="onRectsChange" />
  </div>
</template>

<script>
import Rectangles from "./YOLOAnnotation/Rectangles.vue";

export default {
  el: "#image-annotation",
  name: "ImageAnnotation",
  components: { Rectangles },
  data: function() {
    return { tempRect: {}, rects: [], drawing: false };
  },
  watch: {
    rects: function() {
      this.init();
    }
  },
  methods: {
    onRectsChange: function(index_checked) {
      var newRects = this.rects.slice();
      newRects[index_checked[0]].isActive = index_checked[1];
      this.rects = newRects;
    },
    drawRect: function(rect) {
      var x = rect.baseX;
      var y = rect.baseY;
      var width = rect.x - rect.baseX;
      var height = rect.y - rect.baseY;
      if (rect.isActive) {
        this.context.strokeRect(x, y, width, height);
        this.context.stroke();
      }
    },
    mouseMove: function(e) {
      if (this.drawing) {
        this.init();
        this.tempRect.x = e.clientX - this.canvas.offsetLeft;
        this.tempRect.y = e.clientY - this.canvas.offsetTop;

        this.drawRect(this.tempRect);
      }
    },
    mouseDown: function(e) {
      this.init();
      this.tempRect.baseX = e.clientX - this.canvas.offsetLeft;
      this.tempRect.baseY = e.clientY - this.canvas.offsetTop;

      this.drawing = true;
    },
    init: function() {
      this.context.clearRect(0, 0, this.canvas.width, this.canvas.height);
      this.rects.map(this.drawRect);
    },
    mouseUp: function() {
      this.drawing = false;
      this.tempRect.isActive = false;
      this.rects.push(this.tempRect);
      this.tempRect = {};
    }
  },
  mounted() {
    this.canvas = this.$refs.canvas;
    this.context = this.canvas.getContext("2d");
    this.canvas.addEventListener("mousemove", this.mouseMove, false);
    this.canvas.addEventListener("mouseup", this.mouseUp, false);
    this.canvas.addEventListener("mousedown", this.mouseDown, false);
  }
};
</script>
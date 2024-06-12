<template>
    <div>
      <h1>Zone de Dessin</h1>
      <canvas
        ref="canvas"
        @touchstart="startDrawing"
        @touchmove="draw"
        @touchend="stopDrawing"
        width="500"
        height="500"
        class="drawing-canvas"
      ></canvas>
      <v-btn color="error" @click="clearCanvas">Effacer le dessin</v-btn>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        isDrawing: false,
        context: null
      };
    },
    mounted() {
      const canvas = this.$refs.canvas;
      this.context = canvas.getContext('2d');
      this.context.lineWidth = 5;
      this.context.lineCap = 'round';
    methods: {
      startDrawing(event) {
        this.isDrawing = true;
        const touch = event.touches[0];
        this.context.beginPath();
        this.context.moveTo(touch.clientX - event.target.offsetLeft, touch.clientY - event.target.offsetTop);
      },
      draw(event) {
        if (!this.isDrawing) return;
        const touch = event.touches[0];
        this.context.lineTo(touch.clientX - event.target.offsetLeft, touch.clientY - event.target.offsetTop);
        this.context.stroke();
      },
      stopDrawing() {
        this.isDrawing = false;
        this.context.closePath();
      },
      clearCanvas() {
        const canvas = this.$refs.canvas;
        this.context.clearRect(0, 0, canvas.width, canvas.height);
      }
    }
  };
  </script>
  
  <style scoped>
  .drawing-canvas {
    border: 1px solid #000;
    touch-action: none; /* Prevent scrolling while drawing */
  }
  </style>
  
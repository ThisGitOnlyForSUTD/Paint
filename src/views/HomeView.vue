<template>
<div class="main">
  <canvas class="canvas" width="700" height="700" ref="canvas" @mousemove="onMouseMove" @mousedown="onMouseDown" @mouseup="onMouseUp"></canvas>
  <input class="range" type="range" min="1" max="19" v-model="paintWidth" step="1">
  <div class="controls">
    <button class="controls__button">Заливка</button>
    <div class="controls__colors">
      <div class="controls__color" @click="changeColor" style="background-color: black"></div>
      <div class="controls__color" style="background-color: white"></div>
      <div class="controls__color" style="background-color: red"></div>
      <div class="controls__color" style="background-color: yellow"></div>
      <div class="controls__color" style="background-color: green"></div>
      <div class="controls__color" style="background-color: blue"></div>
      <div class="controls__color" style="background-color: deepskyblue"></div>
      <div class="controls__color" style="background-color: violet"></div>
      <div class="controls__color" style="background-color: orange"></div>
    </div>
    <button class="controls__button">Режим</button>
  </div>
</div>
</template>

<script>
export default {
  name: "HomeView.vue",
  data () {
    return {
      painting: false,
      paintWidth: 10,
      ctx: null,
    }
  },
  mounted() {
    this.ctx = this.$refs.canvas.getContext('2d')
  },
  methods: {

    onMouseMove(e) {
      let offsetX = e.offsetX
      let offsetY = e.offsetY
      if(!this.painting) {
        this.ctx.beginPath()
        this.ctx.moveTo(offsetX,offsetY)
      } else {
        this.ctx.lineTo(offsetX,offsetY)
        this.ctx.strokeStyle = '#2c2c2c'
        this.ctx.lineWidth = this.paintWidth
        this.ctx.stroke()
      }
    },
    onMouseDown() {
      this.painting = true
      console.log(this.painting)
    },
    onMouseUp() {
      this.painting = false
    }
  },
}

</script>

<style scoped lang="scss">
  .main {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 50px 0;
    margin: 0 auto;
    width: 100%;
    max-width: 1400px;
  }

  .range {
    margin-top: 30px;
  }

  .canvas {
    width: 100%;
    max-width: 700px;
    height: 700px;
    background-color: white;
    border-radius: 15px;
    box-shadow: 0px 5px 21px -5px rgba(34, 60, 80, 0.6);
  }

  .controls {
    margin-top: 20px;
    display: flex;
    justify-content: space-between;
    &__button {
      padding: 5px 10px;
      text-align: center;
      border-radius: 10px;
      background-color: aquamarine;
    }
    &__colors{
      display: flex;
      padding: 0 30px;
    }
    &__color {
      cursor: pointer;
      width: 50px;
      height: 50px;
      border-radius: 25px;
      box-shadow: 0px 5px 21px -5px rgba(34, 60, 80, 0.6);
    }
  }
</style>
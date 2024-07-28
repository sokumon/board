<template>
  <div class="flex justify-center items-center h-screen bg-gray-100">
    <canvas
      ref="canvas"
      id="hello"
      class="border border-gray-400"
      width="800"
      height="600"
    ></canvas>
  </div>
</template>

<script>
export default {
  name: 'FabCanvas',
  mounted() {
    this.canvas = new this.fabric.Canvas('hello')

    // Add a rectangle
    const rect = new fabric.Rect({
      left: 100,
      top: 100,
      fill: 'red',
      width: 200,
      height: 200,
    })

    this.canvas.add(rect)
  },
  data() {
    return {
      canvas: null,
    }
  },
}
</script>

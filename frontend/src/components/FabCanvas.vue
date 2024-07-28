<template>
  <div class="flex w-full">
    <canvas
      ref="canvas"
      id="hello"
      :width="canvas_width"
      :height="canvas_height"
      class="flex-col w-full overflow-y-auto"
    ></canvas>

    <div class="flex flex-col gap-5 items-center">
      <div @click="clickHandler" v-for="tool in tools" :id="tool.name">
        {{ tool.name }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'FabCanvas',
  data() {
    return {
      canvas: null,
      canvas_width:window.innerWidth - 100,
      canvas_height:window.innerHeight,
      tools:[
          {
              name:"Pencil",
          },{
            name:"WColor",
          },
          {
            name:"Spray",
          },
          {
              name:"Move",
          },
          {
              name:"Note",
          },
          {
              name:"Triangle",
          },
          {
            name:"Square",
          },
          {
            name:"Circle"
          },
          {
          name:"Erase",
          },
  ],
    }
  },
  methods:{
    clickHandler(event){
    console.log(event.target.id)
    if (event.target.id === "WColor"){
      this.canvas.
    }

  }
},
  mounted() {
  this.canvas = new this.fabric.Canvas('hello')
  // Adjust canvas size to match the window size
    // Add a rectangle
    const rect = new fabric.Rect({
      left: 0,
      top: 100,
      fill: 'blue',
      width: 200,
      height: 200,
    })

    this.canvas.add(rect)
  },
  computed(){

  }
}
</script>

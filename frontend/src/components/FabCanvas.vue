<template>
  <div class="flex w-full">
    <canvas
      ref="canvas"
      id="hello"
      :width="canvas_width"
      :height="canvas_height"
      class="flex-col w-full overflow-y-auto"
    ></canvas>

    <div class="flex flex-col gap-5 p-4 items-center">
      <h1 class="text-xl">Tools</h1>
      <div
        @click="clickHandler"
        @mouseup="save_draw"
        v-for="tool in tools"
        :id="tool.name"
      >
        {{ tool.name }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "FabCanvas",
  data() {
    return {
      canvas_width: window.innerWidth - 100,
      canvas_height: window.innerHeight,
      tools: [
        {
          name: "Pencil",
        },
        {
          name: "WColor",
        },
        {
          name: "Spray",
        },
        {
          name: "Move",
        },
        {
          name: "Text",
        },
        {
          name: "Triangle",
        },
        {
          name: "Rect",
        },
        {
          name: "Circle",
        },
        {
          name: "Erase",
        },
        {
          name: "Clear",
        },
      ],
    }
  },
  mounted() {
    this.canvas = new this.fabric.Canvas("hello")
    if (localStorage.getItem("canvasState")) {
      let canvas_json = localStorage.getItem("canvasState")
      this.canvas.loadFromJSON(canvas_json)
    }

    // Adjust canvas size to match the window size
    // Add a rectangle
  },
  methods: {
    clickHandler(event) {
      this.canvas.on("mouse:up", this.save_draw())
      console.log(event.target.id)
      if (event.target.id === "WColor") {
        this.canvas.freeDrawingBrush = new fabric.CircleBrush(this.canvas)
        this.canvas.freeDrawingBrush.width = 35
        this.canvas.isDrawingMode = true
      }
      if (event.target.id === "Pencil") {
        this.canvas.freeDrawingBrush = new fabric.PencilBrush(this.canvas)
        this.canvas.freeDrawingBrush.width = 10
        this.canvas.isDrawingMode = true
      }
      if (event.target.id === "Erase") {
        this.canvas.freeDrawingBrush = new fabric.EraserBrush(this.canvas)
        this.canvas.freeDrawingBrush.width = 10
        this.canvas.isDrawingMode = true
      }

      if (event.target.id === "Spray") {
        this.canvas.freeDrawingBrush = new fabric.SprayBrush(this.canvas)
        this.canvas.freeDrawingBrush.width = 10
      }

      if (event.target.id === "Rect") {
        this.canvas.isDrawingMode = false
        const rect = new fabric.Rect({
          left: 0,
          top: 100,
          fill: "blue",
          width: 200,
          height: 200,
          erasable: false,
          selectable: true,
          hasControls: true,
          hasBorders: true,
          evented: true,
        })
        console.log(rect)
        this.canvas.add(rect)
      }

      if (event.target.id === "Move") {
        this.canvas.isDrawingMode = false
        let all_objects = this.canvas.getObjects()
        if (all_objects.length > 0) {
          for (let i = 0; i < all_objects.length; i++) {
            all_objects[i].selectable = true
            all_objects[i].hasControls = true
            all_objects[i].hasBorders = true
          }
        }
      }

      if (event.target.id === "Triangle") {
        this.canvas.isDrawingMode = false
        var triangle = new fabric.Triangle({
          width: 150,
          height: 100,
          fill: "",
          stroke: "green",
          strokeWidth: 3,
          cornerColor: "blue",
          angle: 45,
          erasable: false,
          selectable: false,
          hasControls: false,
          hasBorders: false,
          evented: true,
        })

        // Render the triangle in canvas
        this.canvas.add(triangle)
        this.canvas.centerObject(triangle)
      }

      if (event.target.id === "Circle") {
        this.canvas.isDrawingMode = false
        var circle = new fabric.Circle({
          left: 300,
          top: 300,
          fill: "yellow",
          radius: 50,
        })
        this.canvas.add(circle)
      }

      if (event.target.id === "Text") {
        this.canvas.isDrawingMode = false
        var textEditable = new fabric.Textbox("Edit me", {
          left: 70,
          width: 500,
          editable: true,
        })

        this.canvas.add(textEditable)
      }

      if (event.target.id === "Clear") {
        this.canvas.clear()
      }
      this.save_draw()
    },
    save_draw() {
      let canvas_json = this.canvas.toJSON()
      console.log()
      if (canvas_json.objects.length > 0) {
        localStorage.setItem("canvasState", JSON.stringify(canvas_json))
      }
    },
  },
}
</script>

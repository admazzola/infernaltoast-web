<template>
  <div v-if="active" class=" absolute border-2 border-black"
 
             ref="draggableContainer"
             style="top:50px;left:50px;"
                            
        >

    <div   @mousedown="dragMouseDown" class="border-b-2 border-black px-2 bg-blue-500 text-white cursor-pointer select-none" style="background:  linear-gradient(to right, rgb(69 121 207) 25%, rgb(109 83 254) 75%);">  <div class="inline mr-2"> {{name}} </div>  <div @click="onActionCallback({type:'closeApplication',name:name})" class="inline bg-white px-1 text-red-500 rounded cursor-pointer hover:bg-gray-400"> ✖️ </div>  </div> 

     <div class=" p-2 bg-gray-100 ">  {{description}}   </div> 
     
   
  </div>
</template>


<script>


export default {
  name: 'ApplicationWindow',
  props: ['active','name','description','thumbnail','hyperlink','onActionCallback'],
  data() {
    return {
      
      positions: {
        clientX: undefined,
        clientY: undefined,
        movementX: 0,
        movementY: 0
      }
       
    }
  },
  created(){


     
  },
  methods: {
   /* dragStart(event){
      console.log('start drag', event.pageX, event.pageY)

    },
    onDrag(event){
        console.log('on drag', event.pageX, event.pageY)

       this.offsetCoords.x=event.pageX
       this.offsetCoords.y=event.pageY

        console.log('on drag',  this.offsetCoords )

    },*/

    dragMouseDown: function (event) {
      event.preventDefault()
      // get the mouse cursor position at startup:

      //console.log("drag1", event )
      this.positions.clientX = event.clientX
      this.positions.clientY = event.clientY
      document.onmousemove = this.elementDrag
      document.onmouseup = this.closeDragElement
    },
    elementDrag: function (event) {
      event.preventDefault()
      this.positions.movementX = this.positions.clientX - event.clientX
      this.positions.movementY = this.positions.clientY - event.clientY
      this.positions.clientX = event.clientX
      this.positions.clientY = event.clientY
      // set the element's new position:
      this.$refs.draggableContainer.style.top = (this.$refs.draggableContainer.offsetTop - this.positions.movementY) + 'px'
      this.$refs.draggableContainer.style.left = (this.$refs.draggableContainer.offsetLeft - this.positions.movementX) + 'px'
    },
    closeDragElement () {
      document.onmouseup = null
      document.onmousemove = null
    }


  }
}
</script>

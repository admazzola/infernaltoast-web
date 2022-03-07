<template>


  <div class=" p-2 text-center  inline-block cursor-pointer " v-on:dblclick="onActionCallback({type:'openApplication', name:name})">

    <img v-bind:src="icon"  class="select-none" style="width:64px;height:64px; margin:0 auto;"  />


    <div class=""> 
     {{name}}

     </div> 


  </div>


</template>


<script>

 
export default {
  name: 'DesktopIcon',
  props: ['name','icon','onActionCallback'],
  data() {
    return {
      
    }
  },
  created(){
 
  },
  methods: {
   
  }
}
</script>

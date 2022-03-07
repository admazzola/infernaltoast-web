<template>
  <div class='absolute z-10'>
    <div v-if="active" class="border-2 border-black bg-gray-400" style="min-width:300px">
  
   
        <div  v-for="item of applicationList" @click="onActionCallback({type:'openApplication',name: item.name})"  class="select-none cursor-pointer p-2 hover:bg-gray-500">

          {{item.name }}

         </div> 


      </div>
  </div>
</template>


<script>

export default {
  name: 'StartMenu',
  props: ["active",'applicationList','onActionCallback'],
  components: {},
  data() {
    return {

    }
  },
  methods: {



  }
}
</script>

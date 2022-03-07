<template>
  <div   class=" truncate border-2 border-gray-500 px-2 cursor-pointer inline mr-2 py-1" style="width:150px" @click="onActionCallback({type:'clickedApplicationTab',label: label})">
    
    {{label}}
   
  </div>
</template>


<script>


export default {
  name: 'ApplicationTab',
  props: ['label','onActionCallback'],
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

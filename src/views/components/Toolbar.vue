<template>
  <div class="w-full bg-gray-400 text-black flex flex-row border-b-2 border-black">

    <div class="flex select-none font-bold border-2 border-black px-2 hover:bg-gray-500 cursor-pointer" @click="onActionCallback({type:'openStartMenu'})"> <img src="/punklogo.png" class="inline-block mt-1 mr-1" style="width:18px;height:18px" />  Start </div> 

    <div class="flex-grow px-2"> 

      
        
        <ApplicationTab
          v-for="item of activeTabsList"
          v-if="item.active"
          v-bind:label="item.name"
          v-bind:onActionCallback="onActionCallback"
        
         /> 
      
      </div> 


       <div class="flex select-none  border-2 border-black px-2 "  >   {{timeFormatted}} </div> 
    
  </div>
</template>


<script>

import ApplicationTab from './ApplicationTab.vue'


export default {
  name: 'Footer',
  props: ['onActionCallback','activeTabsList'],
  components:{ApplicationTab},
  data() {
    return {
      timeFormatted: '1:02'
    }
  },
  created(){
    this.updateTime()
    setInterval(this.updateTime, 5000)
  },
  methods: {
      updateTime(){
        var d = new Date();    
        this.timeFormatted =  d.toLocaleTimeString([], {hour: '2-digit', minute:'2-digit'});  // -> "7:38:05 AM" 


    }
  }
}
</script>

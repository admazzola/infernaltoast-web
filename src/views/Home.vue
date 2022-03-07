<template>

<div>

  <Toolbar
    v-bind:onActionCallback="onToolbarAction"
    v-bind:activeTabsList="applicationList"
  
   /> 

   <div class=" relative ">

     <StartMenu 
      v-bind:active="startMenuActive"
      v-bind:applicationList="applicationList"
      v-bind:onActionCallback="onStartMenuAction"
     /> 

     <ApplicationWindow
      v-for="item of applicationList"
      v-bind:name="item.name"
      v-bind:thumbnail="item.thumbnail"
      v-bind:hyperlink="item.hyperlink"
      v-bind:description="item.description"
      v-bind:active="item.active"
      v-bind:onActionCallback="onWindowAction"
      
     
      /> 

     <div class="p-4 ">
       
       
        <DesktopIcon 
          v-for="item of applicationList"

          v-bind:name="item.name" 
          v-bind:icon="item.icon"        
          v-bind:onActionCallback="onIconAction"
        
        /> 
        
        
      </div> 


    

    

   </div>


   

   

  
</div>
</template>


<script>
import Toolbar from './components/Toolbar.vue'; 
import StartMenu from './components/StartMenu.vue'; 
import DesktopIcon from './components/DesktopIcon.vue'; 
import ApplicationWindow from './components/ApplicationWindow.vue'; 

const ApplicationList = require('./config/AppConfig.json')

export default {
  name: 'Home',
  props: [],
  components: {Toolbar,DesktopIcon,StartMenu,ApplicationWindow},
  data() {
    return {
      startMenuActive: false,
      //activeTabsList:[],
      applicationList: []
    }
  },
  created(){

    this.applicationList = [];

    for(let app of ApplicationList){
      app.active = false;
      this.applicationList.push(app);
    }
   

  },
  methods: {

    onToolbarAction(action){
      console.log('onToolbarAction',action)

      if(action.type == 'openStartMenu'){
        this.toggleStartMenu()
      }
    },
    onIconAction(action){
         
        if(action.type == 'openApplication'){
          this.openApplication(action.name)
        }

    },
    onStartMenuAction(action){
       
        if(action.type == 'openApplication'){
          this.openApplication(action.name)
        }

       this.startMenuActive=false;

    },
    onWindowAction(action){
      if(action.type == 'closeApplication'){
          this.closeApplication(action.name)
        }
    },

    toggleStartMenu(){
      this.startMenuActive=!this.startMenuActive;
    },
    openApplication(appName){
      for(let i in this.applicationList){
        let app = this.applicationList[i]
        if(!app.active && app.name == appName){


          //for now 
          this.routeTo(app.hyperlink)
          return 

          app.active = true;
        }
      }
    },
    closeApplication(appName){
      for(let i in this.applicationList){
        let app = this.applicationList[i]
        if(app.active && app.name == appName){
          app.active = false;
        }
      }

    },
  routeTo(uri){
        window.open(uri, "_blank");
  }
  }
}
</script>

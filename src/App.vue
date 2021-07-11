<template>
  <div class="w-full h-full m-auto font-noto" :class="{'xs:max-w-xs p-3':landscape}">
    <div id="phone" class="w-full h-full bg-cover overflow-hidden relative" :class="{'xs:rounded-lg':landscape}">
      <!-- desktop -->
      <div class="w-full h-full flex flex-col ">
        <!-- app list -->
        <div class="flex-grow p-3">
          <div class="w-full h-20 p-1 grid grid-cols-4 gap-2">
            <div class="w-full flex justify-center" v-for="app in appsList()" :key="'div-'+app.hashID">
              <Application v-bind="app" :key="app.name+app.hashID"  @click="openedApp = app;openedApp.openTime = new Date().getTime()" />
            </div>
          </div>
        </div>
        <!-- dock -->
        <div class="w-full p-3">
          <div class=" bg-white/30 w-full h-20 rounded-3xl flex justify-between p-3">
            <Application v-for="app in appsInDockList()" v-bind="app" :key="app.name+app.hashID" @click="openedApp = app;openedApp.openTime = new Date().getTime()" />
            <Application v-bind="fullScreenApp" @click="fullScreen()" />
          </div>
        </div>
      </div>
      <ApplicationWindow v-bind="openedApp" @appClosed="appClose()" />
    </div>
  </div>
</template>

<script>
import Application from './components/Application.vue'
import ApplicationWindow from './components/ApplicationWindow.vue'

// This starter template is using Vue 3 experimental <script setup> SFCs
// Check out https://github.com/vuejs/rfcs/blob/script-setup-2/active-rfcs/0000-script-setup.md
export default {
  data(){
    return {
      landscape: false,
      apps:[
        // in docks
        {
          name:'Tailwind CSS',
          hashID:"dfa32r1fsb35ga243",
          bgColor:"#ffffff",
          url:"https://tailwindcss.tw",
          inDock: true,
          padding:true,
          openTime:false
        },
        {
          name:'欠人教訓的提問 & 發問',
          icon:'./icons/ray-xu.png',
          hashID:"fsb35ga243dfa32r1",
          bgColor:"#ffffff",
          url:"https://hsiangfeng.github.io/learnexp/20200112/1752686187/",  
          inDock: true,
          padding:false,
          openTime:false
        },
        {
          name:'粉絲專頁',
          icon:'./icons/facebook.svg',
          hashID:"fsb3asfasfdfa32r1",
          bgColor:"#ffffff",
          url:"https://www.facebook.com/plugins/page.php?href=https%3A%2F%2Fwww.facebook.com%2Flalarabbits-%25E5%2585%2594%25E5%2585%2594%25E6%2595%2599%25E5%25A4%25A7%25E6%259C%25AC%25E7%2587%259F-102150975410839&tabs=timeline&width=320&height=1000&small_header=false&adapt_container_width=true&hide_cover=false&show_facepile=true&appId",  
          inDock: true,
          padding:false,
          openTime:false
        },

        // in list
        {
          name:'菜兔餐廳',
          icon:'./icons/google.svg',
          hashID:"fsbkgkfmtk43dfa32r1",
          bgColor:"#ffffff",
          url:"https://lavuta-restaurant.herokuapp.com/",  
          inDock: false,
          padding:true,
          openTime:false
        },
        {
          name:'如何自主學習',
          icon:'./icons/youtube.svg',
          hashID:"fsb3dghb15452632r1",
          bgColor:"#ffffff",
          url:"https://www.youtube.com/embed/7DUUCEGkYs4",
          inDock: false,
          padding:true,
          openTime:false
        },
        {
          name:'公版圖',
          icon:'./icons/hackmd.png',
          hashID:"fsb35ga2sfdb6511",
          bgColor:"#ffffff",
          url:"https://hackmd.io/@lalarabbits/rykaZuWpu",  
          inDock: false,
          padding:false,
          openTime:false
        },
        {
          name:'台北天氣',
          icon:'./icons/weather.svg',
          hashID:"fsdfbsdfb6ga243dfa32r1",
          bgColor:"#0066CC",
          url:"https://www.cwb.gov.tw/V8/C/W/County/County.html?CID=63",  
          inDock: false,
          padding:false,
          openTime:false
        },
        {
          name:'pretending-app',
          icon:'./icons/clock.svg',
          hashID:"243dfafsb35ga32r1",
          bgColor:"#408080",
          url:"https://pretending-app.vercel.app/#/worldClock",  
          inDock: false,
          padding:false,
          openTime:false
        }
      ],
      fullScreenApp:{
        name:'fullscreen-tool',
        icon:'./icons/fullscreen.svg',
        hashID:"dfafsb35243ga32r1",
        bgColor:"white",
        url:"",  
        inDock: true,
        padding:true,
        openTime:false
      },    
      openedApp:null,
      open: false,
      fullscreen: false,
    }
  },
  mounted(){
    // if(screen.width>screen.height){
    //   console.log(`${screen.width}>${screen.height}`)
    //   this.landscape = true
    // }
    this.resize()
    window.addEventListener('resize', this.resize)
  },
  methods:{
    appsInDockList(){
      return this.apps.filter((app)=>{ return app.inDock })
    },
    appsList(){
      return this.apps.filter((app)=>{ return !app.inDock })
    },
    appClose(){
      this.open = false
    },
    resize(){
      const w = window.innerWidth
      const h = window.innerHeight

      const aspectRatio = Math.round(h/w*1000)/1000
      
      if(w>h){
        this.landscape = true
      }else{
        if(aspectRatio<1.4){
          this.landscape = true
        }else{
          this.landscape = false
        }
      }
    },
    fullScreen(){
      this.fullscreen = !this.fullscreen
      
      const page = document.documentElement
      if(page.requestFullscreen && !this.fullscreen){
        this.fullScreenApp.icon = "./icons/screen-back.svg"
        page.requestFullscreen()
      }else if(document.exitFullscreen && this.fullscreen){
        this.fullScreenApp.icon = "./icons/fullscreen.svg"
        document.exitFullscreen()
      }
    }
  },
  components:{
    Application,ApplicationWindow
  }
}

</script>

<style scoped>
  #phone {
    background-image: url('./assets/bg.jpg');
  }
</style>
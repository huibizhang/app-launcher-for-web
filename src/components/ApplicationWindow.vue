<template>
  <div
    class="bg-black transition-all z-10"
    :class="{
      'w-0 h-0': !open,
      'w-full h-full absolute rounded-none': open,
      'top-full left-1/2 opacity-0 duration-500': animation,
      'top-0 left-0 opacity-100 duration-500': !animation,
    }"
  >
    <div class="w-full h-full relative">
      <div class="w-full h-full bg-black flex flex-col absolute">
        <div class="flex-grow">
          <iframe v-if="contentLoad" :src="url" class="w-full h-full"></iframe>
        </div>
        <div class="p-1 text-center overflow-hidden" @click="appClose()">
          <div class="w-2/5 h-1 bg-white rounded-full m-auto my-0.5"></div>
          <!-- <span class="text-white text-xs">[ Click me to close App ]</span> -->
        </div>
      </div>
      <div
        v-if="open&&!finish"
        :id="'slpashScreen-' + hashID"
        class="
          w-full
          h-full
          flex
          justify-center
          items-center
          transition-all
          duration-1000
          absolute
        "
        :class="{ 'opacity-0': start }"
        :style="'background-color:' + bgColor"
        @click="appOpen()"
      >
        <img
          :src="icon"
          class="object-contain"
          :class="{
            'w-full h-full': !open,
            'p-3': !open && padding,
            'w-1/3 h-full p-0': open,
          }"
        />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ApplicationWindow",
  props: {
    icon: {
      type: String,
      default: "./icons/carrot.svg",
    },
    name: {},
    hashID: {},
    bgColor: {},
    url: {},
    inDock: {},
    padding: {},
    openTime:{},
  },
  data() {
    return {
      open: false,
      loading: true,
      start: false,
      finish: true,
      animation: true,
      contentLoad: false,
    };
  },
  watch: {
    openTime: "appOpen",
  },
  methods: {
    appOpen() {
      if (!this.finish || !this.hashID) {
        return;
      }
      this.finish = false;
      this.open = true;
      this.animation = false;
      if (this.open) {
        setTimeout(this.starting, 1500);
        setTimeout(this.loadingFinish, 2500);
      }
    },
    appClose() {
      this.open = false;
      this.start = false;
      this.loading = true;
      this.animation = true;
      this.contentLoad = false;
      this.$emit("appClosed");
    },
    starting() {
      this.start = true;
      this.contentLoad = true;
    },
    loadingFinish() {
      this.loading = false;
      this.finish = true;
    },
  },
};
</script>

<style></style>

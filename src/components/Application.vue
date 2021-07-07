<template>
  <div class="w-14" :class="{ 'h-14': inDock, 'h-20': !inDock }">
    <div class="w-14 h-14 relative rounded-xl overflow-hidden">
      <div
        :id="'slpashScreen-' + hashID"
        class="
          w-full
          h-full
          flex
          justify-center
          items-center
          transition-all
          duration-1000
        "
        :style="'background-color:' + bgColor"
      >
        <img
          :src="icon"
          class="object-contain w-full h-full"
          :class="{
            'p-3': padding,
          }"
        />
      </div>
    </div>
    <div
      v-if="!inDock"
      class="
        w-16
        h-6
        -mx-1
        leading-6
        text-xs text-center
        overflow-hidden overflow-ellipsis
        whitespace-nowrap
      "
    >
      {{ name }}
    </div>
  </div>
</template>

<script>
export default {
  name: "Application",
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
  },
  data() {
    return {

    }
  },
  methods: {
    
  },
}
</script>

<style></style>

<template lang="html">
  <div class="example-node relative  bg-white rounded border border-gray-300"
  :style="{ width: `${width}px`} ">
    <div class="flex flex-col border-b border-gray-300">
      <div class="flex flex-row flex-no-wrap justify-between items-center p-4">
        <div class="flex flex-row flex-no-wrap justify-start items-center">
          <div class="flex-shrink bg-blue-2 mr-2">
            <img :src="`demo_assets/${icon}.svg`" />
          </div>
          <div class="font-bold text-md text-gray-800">
            {{ title }}
            <span class="text-xs text-gray-400">node id: {{ node.id }}</span>
          </div>
        </div>

        <div @click.stop="dropdown = !dropdown">
          <flowy-drag-handle>
            <img :src="`demo_assets/grabme.svg`" />
          </flowy-drag-handle>
          <div class="relative z-50 -ml-10 py-2 bg-white shadow rounded text-xs" v-show="dropdown" v-click-outside="handleOutside" v-if="node.parentId != -1">
            <span class="cursor-pointer p-2 hover:bg-gray-200 block" @click="remove()">Enter</span>
            <span class="cursor-pointer p-2 hover:bg-gray-200 block" @click="remove()">Edit</span>
            <span class="cursor-pointer p-2 hover:bg-gray-200 block" @click="remove()">Delete</span>
          </div>
        </div>
      </div>
    </div>

    <div class="flex flex-row flex-no-wrap ml-4 mb-4">
      <div class="flex-grow flex flex-col">
        <div class="mt-2 text-sm text-gray-700" v-html="description">

        </div>
      </div>
    </div>
  </div>
</template>

<style lang="scss">
.example-node {
  width: 320px;
}
span.block {
    display:block;
}
.bg-white {
  background-color: #ffffff;
}
// Disables text highlighting
body {
  -webkit-user-select: none;
     -moz-user-select: -moz-none;
      -ms-user-select: none;
          user-select: none;
}
</style>

<script>
import ClickOutside from 'vue-click-outside';

/* eslint-disable no-unused-vars */

export default {

  directives: {
    ClickOutside,
  },

  props: {
    width: {
      default: 200,
    },
    remove: {
      type: Function,
      required: true,
    },
    node: {
      type: Object,
      required: true,
    },
    icon: {
      type: String,
      required: true,
    },
    title: {
      type: String,
      required: true,
    },
    description: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      dropdown: false,
    };
  },
  mounted() {

  },
  destroyed() {

  },
  methods: {

    handleOutside() {
      if (this.dropdown === true) {
        this.dropdown = false;
      }
    },

  },
};
</script>

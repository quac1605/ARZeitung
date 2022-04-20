<template>
  <q-page class="flex flex-center ">
    <model-viewer
      id="preloading"
      src="assets/models/gray_rhino/scene.gltf"
      ios-src="assetss/models/gray_rhino/Gray_Rhino.usdz"
      camera-controls
      auto-rotate
      ar
      reveal="auto"
      style="min-height: 550px; min-width: 450px"
    >
      <q-btn
        slot="ar-button"
        align="center"
        rounded
        class="q-mr-sm q-pa-sm"
        push
        dense
        style=" position: fixed;
        top: 90%;
        left: 50%;
        -webkit-transform: translate(-50%);
        transform: translate(-50%, -50%);"
        @click="showURL"
      >
        <q-icon
          left
          size="1.5em"
          name="mdi-nature-people"
        ></q-icon>
        <div>Let's see in reality</div>
      </q-btn>
      <q-btn
        slot="exit-webxr-ar-button"
        rounded
        style="position: absolute; top: 16px; right: 16px;"
        flat
        dense
        ripple="{ center: true }"
      >
        <q-icon
          left
          size="3em"
          name="mdi-keyboard-backspace"
        ></q-icon>
        <div>Back to viewer</div>
      </q-btn>
    </model-viewer>
    <q-btn
      @click="
        backToHomePage"
      align="center"
      rounded
      class="z-top q-mr-sm q-pa-sm "
      flat
      dense
      icon="mdi-home"
      ripple="{ center: true }"
      style=" position: fixed;
        top: 95%;
        left: 50%;
        -webkit-transform: translate(-50%);
        transform: translate(-50%, -50%);"
    ></q-btn>
  </q-page>

</template>

<script>

import '@google/model-viewer'
import { computed } from '@vue/runtime-core';
// console.log(window.location);
// setTimeout(window.location.replace('https://localhost:8081/#/model-viewer'), 5000);

export default {
  name: 'ModelViewerPage',
  methods: {
    backToHomePage () {
      window.location.reload();
    },
    showURL () {
      console.log(window.location.href);
    }
  },
}
</script>
<style>
model-viewer {
  --poster-color: transparent;
}
</style>

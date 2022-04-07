<template>
  <q-page class="flex flex-center">
    <model-viewer
      src="assets/gray_rhino/scene.gltf"
      camera-controls
      auto-rotate
      ar
      reveal="auto"
      style="height: 550px; width: 500px"
    ></model-viewer>
    <q-btn></q-btn>
  </q-page>
</template>

<script>

import '@google/model-viewer'
export default {
  name: 'ModelViewerPage',
  components: {

  }
}
</script>


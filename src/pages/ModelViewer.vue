<template>
  <q-page class="flex flex-center">
    <model-viewer
      src="assets/gray_rhino/scene.gltf"
      camera-controls
      auto-rotate
      ar
    ></model-viewer>
  </q-page>
</template>

<script>

import '@google/model-viewer'
export default {

  components: {

  }
}
</script>

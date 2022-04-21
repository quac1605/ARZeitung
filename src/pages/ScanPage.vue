<template >
  <q-page class="full-height">
    <div id="ar-container">

      <div class="col-md-12 box stack-top z-top">
        <q-btn
          align="left"
          rounded
          class=" z-top q-mr-sm q-pa-sm map-btn"
          :style="{visibility: isActive ? 'visible' : 'hidden'}"
          flat
          dense
          icon="mdi-weather-cloudy white"
          label="Weather"
          ripple="{ center: true }"
        />
        <br>
        <br>
        <q-btn
          align="left"
          rounded
          class=" z-top q-mr-sm q-pa-sm map-btn"
          :style="{visibility: isActive ? 'visible' : 'hidden'}"
          flat
          dense
          icon="mdi-home-search"
          label="Immobilien"
          ripple="{ center: true }"
        />
        <br>
        <br>
        <q-btn
          align="left"
          rounded
          class="z-top q-mr-sm q-pa-sm map-btn"
          :style="{visibility: isActive ? 'visible' : 'hidden'}"
          flat
          dense
          icon="mdi-card-account-details-outline"
          label="Jobs"
          ripple="{ center: true }"
        />
      </div>
      <!-- <q-btn @click="showMarker = !showMarker">Click di</q-btn>
    <q-btn @click="showMap = !showMap">Click di</q-btn> -->
      <!-- <model-viewer
        v-if="markerDetected"
        class="z-top centered"
        src="assets/gray_rhino/scene.gltf"
        camera-controls
        auto-rotate
        ar
        reveal="auto"
        ar-modes="webxr scene-viewer quick-look"
        poster="assets/images/nicht.png"
      ></model-viewer> -->
    </div>
  </q-page>
</template>

<script>
import { defineComponent } from 'vue';
import '../../public/libs/mindar/mindar-image-three.prod.js'
//import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls'
import { GLTFLoader } from "../../public/libs/three.js-r132/examples/jsm/loaders/GLTFLoader.js";
import { loadGLTF, loadAudio, loadVideo } from "../../public/libs/loader.js"

// import '@google/model-viewer'
const THREE = window.MINDAR.IMAGE.THREE;
const mindarThree = new window.MINDAR.IMAGE.MindARThree({
  container: document.body,
  imageTargetSrc: 'assets/targets/target...',
  maxTrack: 3,
});
const {renderer, scene, camera} = mindarThree;
const sizes = {
  width: window.innerWidth,
  height: window.innerHeight
}

window.addEventListener('resize', () => {
  //update sizes
  sizes.height = window.innerHeight
  sizes.width = window.innerWidth

  //update renderer
  renderer.setSize(sizes.width, sizes.height)
})

export default {
  name: 'ScanPage',
  // components: {

  // },


  data () {
    return {
      isActive: false,
      scene: null,
      camera: null,
      renderer: null,
      light: null,
      material: null
    }
  },

  mounted () {
    this.init()
  },

  methods: {
    async init () {

      // 3D Modelle Loader
      const kiel_hofe = await loadGLTF("/assets/modesl/kielhofe/2022_04_01_Neubauten_KielHoefe_ohneAnimation_mitGreyMaterial.gltf");
      kiel_hofe.scene.scale.set(0.0005, 0.0005, 0.0005);
      kiel_hofe.scene.rotation.x = Math.PI/2;
      kiel_hofe.scene.rotation.y = Math.PI;
      kiel_hofe.scene.position.set(0, 0, 0)
      kiel_hofe.scene.userData.clickable = true;

      //Audio Loader

      //Video Loader

      //Anchor Creating
      const anzeige_Anchor = mindarThree.addAnchor(0);

      anzeige_Anchor.onTargetFound = () => {

        this.$emit('model-viewer');

        // this.$router.push('/model-viewer');

      }
      anzeige_Anchor.onTargetLost = () => {

        this.isActive = false;

      }

      const clock = new THREE.Clock();

      // start AR

      renderer.setAnimationLoop(() => {

        const delta = clock.getDelta
        renderer.render(scene, camera);
      });
      await mindarThree.start();

    }
  }
}
// document.querySelector('#default-poster').style.backgroundColor = 'transparent';
</script>"
<style>
#ar-container {
  min-height: 667px;
}
.centered {
  position: fixed;
  top: 50%;
  left: 50%;
  /* bring your own prefixes */
  transform: translate(-50%, -50%);
}
</style>


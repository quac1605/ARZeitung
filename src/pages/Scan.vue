<template>
  <q-page class="flex flex-center">
    <div class="container">
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



export default {
  // name: 'PageIndex',
  // components: {

  // },


  data () {
    return {
      isActive: false,
      scene: null,
      camera: null,
      sceneCanvas: null,
      renderer: null,
      light: null,
      material: null,
      // markerDetected: false

    }
  },

  mounted () {
    this.init()
  },

  methods: {
    async init () {
      const mindarThree = new window.MINDAR.IMAGE.MindARThree({
        container: document.body,
        imageTargetSrc: '/assets/targets/group_target.mind',
        maxTrack: 2,

      });
      const { renderer, scene, camera } = mindarThree;


      const light = new THREE.HemisphereLight(0xfffff, 0xbbbbff, 1);
      scene.add(light);

      // 3D Modelle, Images, Video Loading

      const markuslowe = await loadGLTF("/assets/models/markuslowe/scene.gltf");
      markuslowe.scene.scale.set(0.3, 0.3, 0.3);
      markuslowe.scene.position.set(0, 0, 0);

      const geometry = new THREE.PlaneBufferGeometry(1, 1, 4, 4);
      const loader = new THREE.TextureLoader();
      const texture = loader.load("/assets/images/kiel_karte.jpg");
      const material_1 = new THREE.MeshBasicMaterial({ map: texture });
      const img = new THREE.Mesh(geometry, material_1);

      const video = await loadVideo("/assets/videos/sintel/sintel.mp4");
      const video_texture = new THREE.VideoTexture(video);
      const video_geometry = new THREE.PlaneGeometry(1, 204 / 480);
      const video_material = new THREE.MeshBasicMaterial({ map: video_texture });
      const video_plane = new THREE.Mesh(video_geometry, video_material);

      //Anchor Creating
      const video_Anchor = mindarThree.addAnchor(0);
      video_Anchor.group.add(video_plane);

      const markuslowe_Anchor = mindarThree.addAnchor(1);
      markuslowe_Anchor.group.add(markuslowe.scene);

      video_Anchor.onTargetFound = () => {
        // video.play();
        //this.isActive = true;
        //this.selectedTab = 'model-viewer';
        //this.$emit('model-viewer');
        // this.markerDetected = true;
        this.$router.push('/model-viewer');
      }
      video_Anchor.onTargetLost = () => {
        // video.pause();
        //this.isActive = false;
        // this.markerDetected = false;
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
.container {
  width: 100%;
  height: 100%;
  position: relative;
  margin: 20px;
  align-self: center;
}
.centered {
  position: fixed;
  top: 50%;
  left: 50%;
  /* bring your own prefixes */
  transform: translate(-50%, -50%);
}
</style>


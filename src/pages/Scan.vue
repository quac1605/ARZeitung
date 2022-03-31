<template>
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
    <div class="box map">
      <l-map
        v-if="showMap"
        style="height: 900px"
        :zoom="zoom"
        :center="center"
        z-index="1"
      >
        <l-tile-layer
          :url="url"
          :attribution="attribution"
        ></l-tile-layer>
        <l-marker :lat-lng="markerLatLng1"></l-marker>
        <l-marker
          :lat-lng="fhKiel"
          :visible="showMarker"
        >
          <l-popup>
            <div>
              <h6>Fachhochschule Kiel</h6>
              <img
                src="https://www.fh-kiel.de/fileadmin/template/images/fachhochschule-kiel-logo.svg"
                style="width: 300px"
              >
              <p>
                Sokratespl. 1, 24149 Kiel
              </p>
              <a href="https://www.fh-kiel.de/startseite/">Website</a>
            </div>
          </l-popup>
        </l-marker>
        <l-marker :lat-lng="markerLatLng3"></l-marker>
        <l-marker :lat-lng="markerLatLng4"></l-marker>
      </l-map>
    </div>
  </div>

</template>

<script>
import { defineComponent } from 'vue';
import '../../public/libs/mindar/mindar-image-three.prod.js'
//import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls'
import { GLTFLoader } from "../../public/libs/three.js-r132/examples/jsm/loaders/GLTFLoader.js";
import { loadGLTF, loadAudio, loadVideo } from "../../public/libs/loader.js"

import "leaflet/dist/leaflet.css"
import { LMap, LTileLayer, LMarker, LPopup } from "@vue-leaflet/vue-leaflet";

const THREE = window.MINDAR.IMAGE.THREE;



export default {
  name: 'PageIndex',
  components: {
    LMap,
    LTileLayer,
    LMarker,
    LPopup
  },
  data () {
    return {
      isActive: false,
      scene: null,
      camera: null,
      sceneCanvas: null,
      renderer: null,
      light: null,
      material: null,

      url: "https://api.maptiler.com/maps/pastel/{z}/{x}/{y}.png?key=rMS7PCdO9WmYpbjBa3N3",
      attribution:
        '&copy; <a target="_blank" href="http://osm.org/copyright">OpenStreetMap</a> contributors',
      zoom: 13,
      center: [54.3224, 10.1331],
      markerLatLng1: [54.3224, 10.1331],
      fhKiel: [54.3325625, 10.1779896],
      markerLatLng3: [54.3275109, 10.1684801],
      markerLatLng4: [54.3162367, 10.1221542],
      showMarker: true,
      showMap: false
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
        this.isActive = true;
        this.showMap = true;
      }
      video_Anchor.onTargetLost = () => {
        // video.pause();
        this.isActive = false;

        this.showMap = false;
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
</script>
<style>
.container {
  width: 100%;
  height: 100%;
  position: relative;
  margin: 20px;
}
.box {
  position: absolute;
  top: 0;
  left: 0;
  opacity: 0.9; /* for demo purpose  */
}
.stack-top {
  z-index: 9;
  margin: 20px; /* for demo purpose  */
  float: right;
  width: 150px;
  height: 200px;
}
.map {
  width: 100%;
  height: 100%;
  z-index: 10;
}
.map-btn {
  width: 150px;
}
</style>

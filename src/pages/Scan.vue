<template>
  <div class="scene">
    <div id="three-scene-canvas"></div>
  </div>
</template>

<script>
import { defineComponent } from 'vue';
import '../../public/libs/mindar/mindar-image-three.prod.js'
//import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls'
import { GLTFLoader } from "../../public/libs/three.js-r132/examples/jsm/loaders/GLTFLoader.js";
import { loadGLTF, loadAudio, loadVideo } from "../../public/libs/loader.js"


const THREE = window.MINDAR.IMAGE.THREE;



export default {
  name: 'PageIndex',
  data () {
    return {
      scene: null,
      camera: null,
      sceneCanvas: null,
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
      const mindarThree = new window.MINDAR.IMAGE.MindARThree({
        container: document.body,
        imageTargetSrc: '/assets/targets/group_target.mind',
        maxTrack: 2,

      });
      const { renderer, scene, camera } = mindarThree;


      const light = new THREE.HemisphereLight(0xfffff, 0xbbbbff, 1);
      scene.add(light);

      // 3D Modelle, Images, Video Loading
      const binocular = await loadGLTF("/assets/models/binoculars/scene.gltf");
      binocular.scene.scale.set(0.2, 0.2, 0.2);
      binocular.scene.position.set(0, 0, 0);

      const markuslowe = await loadGLTF("/assets/models/markuslowe/scene.gltf");
      markuslowe.scene.scale.set(0.3, 0.3, 0.3);
      markuslowe.scene.position.set(0, 0, 0);

      const rain = await loadGLTF("/assets/models/rain_2/scene.gltf");
      rain.scene.scale.set(0.05, 0.05, 0.05);
      rain.scene.position.set(0, -2.5, 0);
      rain.scene.rotation.set(0, 0, Math.PI / 2);

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

      //Sound Loading
      const rain_Audio = await loadAudio("/assets/sounds/rain.mp3");
      const listener = new THREE.AudioListener();
      const audio = new THREE.PositionalAudio(listener);
      audio.setRefDistance(100);
      audio.setBuffer(rain_Audio);
      audio.setLoop(true);

      //Anchor Creating
      const binocular_Anchor = mindarThree.addAnchor(0);
      binocular_Anchor.group.add(video_plane);

      const markuslowe_Anchor = mindarThree.addAnchor(1);
      markuslowe_Anchor.group.add(markuslowe.scene);

      const rain_Anchor = mindarThree.addAnchor(2);
      rain_Anchor.group.add(rain.scene);
      rain_Anchor.group.add(img);

      camera.add(listener);
      rain_Anchor.group.add(audio);

      rain_Anchor.onTargetFound = () => { audio.play(); }
      rain_Anchor.onTargetLost = () => { audio.pause(); }

      binocular_Anchor.onTargetFound = () => { video.play(); }
      binocular_Anchor.onTargetLost = () => { video.pause(); }

      //Animation Editing
      const mixer = new THREE.AnimationMixer(rain.scene);
      const action = mixer.clipAction(rain.animations[0]);
      action.play();


      const clock = new THREE.Clock();

      // start AR

      renderer.setAnimationLoop(() => {

        const delta = clock.getDelta
        rain.scene.rotation.set(0, rain.scene.rotation.y + delta, 0);
        mixer.update(delta)
        renderer.render(scene, camera);
      });
      await mindarThree.start();

    }
  }
}
</script>

<template >
  <q-page class="full-height">
    <div id="ar-container">
    </div>
  </q-page>
</template>

<script>
import { defineComponent } from 'vue';
import '../../public/libs/mindar/mindar-image-three.prod.js'
import { loadGLTF, loadAudio, loadVideo } from "../../public/libs/loader.js"

// import '@google/model-viewer'
const THREE = window.MINDAR.IMAGE.THREE;



export default {
  name: 'ScanPage',
  data () {
    return {
      videoOnPlay: false,
      threeDmodelOnPlay: false,
      modelviewerOnPlay: false
    }
  },
  mounted () {
    this.init()
  },
  methods: {
    async init () {
      const mindarThree = new window.MINDAR.IMAGE.MindARThree({
        container: document.getElementById("ar-container"),
        //container: document.body,
        imageTargetSrc: '/assets/targets/marker_final02.mind',
        maxTrack: 4,

      });
      const { renderer, scene, camera } = mindarThree;
      // Open Model Viewer with an Marker
      const anzeige_Anchor = mindarThree.addAnchor(0);

      anzeige_Anchor.onTargetFound = () => {
        if (this.videoOnPlay != true) {
          this.$emit('model-viewer');
          console.log("anzeige target found");
        }
        console.log("anzeige target found");
        this.modelviewerOnPlay = true;
      }
      anzeige_Anchor.onTargetLost = () => {
        console.log("anzeige target lost");
        this.modelviewerOnPlay = false;
      }
      // Open Video
      const video = await loadVideo("assets/videos/InterviewVideo.mp4");
      const texture = new THREE.VideoTexture(video);
      const geometry = new THREE.PlaneGeometry(1, 1);
      const material = new THREE.MeshBasicMaterial({ map: texture });
      const plane = new THREE.Mesh(geometry, material);
      const video_Anchor = mindarThree.addAnchor(1);
      video_Anchor.group.add(plane)
      video_Anchor.onTargetFound = () => {
        this.videoOnPlay = true;
        console.log("video target found");
        video.play();
      }

      video_Anchor.onTargetLost = () => {
        this.videoOnPlay = false;
        video.pause();
        console.log("video target lost");
        // If Anzeige is in the frame when the video target lost then play the model-viewer
        if (this.modelviewerOnPlay == true) {
          this.$emit('model-viewer');
        }

      }

      video.addEventListener("play", () => {
        video.currentTime = 6;
      })
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


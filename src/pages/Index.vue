<template>
  <q-page>
    <div>
      <q-dialog
        v-model="prompt"
        persistent
        class="dialog q-pr-none"
      >
        <q-card
          style="min-width: 350px"
          class="bg-grey-4 "
        >

          <q-card-actions
            align="center"
            class="text-primary q-pt-none q-pr-none"
          >

            <q-card-section class=" q-pl-none q-pt-none q-pr-none">
              <q-list>
                <q-item
                  clickable
                  v-ripple
                  class="text-dark q-pl-none q-pt-none q-pr-none"
                  align="center"
                >
                  <q-item-section class="q-pt-none">
                    <div><a href="https://holonative.de/ueber-uns/"><img
                          src="https://holonative.de/wp-content/uploads/2020/06/holoNative_1000px_333px.png"
                          width="360"
                        ></a></div>
                  </q-item-section>
                </q-item>
                <q-item
                  clickable
                  v-ripple
                  class="text-dark text-weight-medium text-h6 q-pl-none q-pr-none"
                  align="left"
                >
                  <q-item-section class="q-pa-sm">
                    Step 1: Allow the website to access your camera
                  </q-item-section>
                </q-item>
                <q-item
                  clickable
                  v-ripple
                  class="text-dark text-weight-medium text-h6 q-pl-none q-pr-none"
                  align="left"
                >
                  <q-item-section class="q-pa-sm">
                    Step 2: Show your camera in front of the picture that you want.
                  </q-item-section>
                </q-item>

                <q-item
                  clickable
                  v-ripple
                  class="text-dark text-weight-medium text-h6 q-pl-none q-pr-none"
                  align="left"
                >
                  <q-item-section class="q-pa-sm">
                    Step 3: Look and interact through the screen of your phone or computer.
                  </q-item-section>
                </q-item>
              </q-list>

            </q-card-section>
          </q-card-actions>
          <q-card-actions
            align="center"
            class="text-primary"
          >
            <q-btn
              v-close-popup
              rounded
              push
              class=" bg-grey-9 text-white text-h6 q-pl-none q-pr-none"
              style="width: 200px"
              @click="choseScanTab"
            >Let's begin</q-btn>
          </q-card-actions>
        </q-card>
      </q-dialog>
    </div>
    <component
      style="height:100%"
      id="setTab"
      :is="selectedTab"
      @model-viewer="changePage"
      @scan="choseScanTab"
    ></component>
  </q-page>

</template>

<script>

import { defineComponent, ref } from 'vue';
import ScanPage from './ScanPage.vue';
import ModelViewerPage from './ModelViewerPage.vue'


import { date } from 'quasar'

export default {
  components: {
    'scan': ScanPage,
    'model-viewer': ModelViewerPage,

  },
  data () {
    return {
      selectedTab: null,
      prompt: true

    };
  },

  methods: {
    changePage () {
      this.selectedTab = 'model-viewer';
      console.log(this.selectedTab);


      //window.location.reload();
      // window.location.href(this.$router.push('/model-viewer'));
      // window.location.reload();
      // this.$router.push('/model-viewer');
    },
    choseScanTab () {
      this.selectedTab = 'scan';
      // this.$router.push('/scan');
    }
  },

}
</script>

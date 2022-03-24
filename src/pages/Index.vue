<template>
  <q-btn
    class="z-top q-ma-sm"
    flat
    dense
    round
    icon="menu"
    aria-label="Menu"
    @click="toggleLeftDrawer"
  />
  <keep-alive>
    <component :is="selectedTab"></component>
  </keep-alive>
  <q-drawer
    v-model="leftDrawerOpen"
    show-if-above
    bordered
    class="bg-indigo-1"
  >

    <q-item class="bg-dark text-white">
      <q-item-section>
        <q-toolbar>

          <q-toolbar-title>
            <img
              src="https://holonative.de/wp-content/uploads/2020/06/holonative_transparent_500px_167px.png"
              alt=""
              height="80"
              width="200"
            >
            <h6 class="q-mt-xs q-mb-xs text-left">
              AR Zeitung Demo
            </h6>

          </q-toolbar-title>

        </q-toolbar>
      </q-item-section>
    </q-item>

    <PageListsHelp></PageListsHelp>
    <PageListsContact></PageListsContact>

  </q-drawer>
  <div class="row float-right">
    <div class="col-md-12">
      <q-btn
        align="left"
        rounded
        class="z-top q-mr-sm q-pa-sm "
        flat
        dense
        icon="mdi-weather-cloudy white"
        label="Weather"
        style="width: 100%;"
        ripple="{ center: true }"
      />
      <br>
      <br>
      <q-btn
        align="left"
        rounded
        class="z-top q-mr-sm q-pa-sm "
        flat
        dense
        icon="mdi-home-search"
        label="Immobilien"
        style="width: 100%;"
        ripple="{ center: true }"
      />
      <br>
      <br>
      <q-btn
        align="left"
        rounded
        class="z-top q-mr-sm q-pa-sm "
        flat
        dense
        icon="mdi-card-account-details-outline"
        label="Jobs"
        style="width: 100%;"
        ripple="{ center: true }"
      />
    </div>
  </div>

</template>

<script>

import { defineComponent, ref } from 'vue';
import Scan from './Scan.vue';


import PageListsHelp from 'src/components/pagelists/PageListsHelp.vue'
import PageListsContact from 'src/components/pagelists/PageListsContact.vue'
import { date } from 'quasar'

export default {
  // provide () {
  //   return {
  //     setSelectedTab: this.setSelectedTab
  //   };
  // },
  components: {
    'scan': Scan,


    PageListsHelp,
    PageListsContact
  },
  data () {
    return {
      selectedTab: 'scan',

    };
  },
  setup () {
    const leftDrawerOpen = ref(false)

    return {

      leftDrawerOpen,
      toggleLeftDrawer () {
        leftDrawerOpen.value = !leftDrawerOpen.value
      }
    }
  },
  computed: {
    todaysDate () {
      const timeStamp = Date.now()
      return date.formatDate(timeStamp, 'dddd D MMMM')
    }
  },
  // methods: {
  //   setSelectedTab (tab) {
  //     this.selectedTab = tab;
  //   },
  // },

}
</script>

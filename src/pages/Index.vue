<template>
  <q-btn
    class="z-top"
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
  >

    <q-item class="bg-grey-3">
      <q-item-section>
        <q-toolbar>

          <q-toolbar-title>
            <h6 class="q-mt-xs q-mb-xs">
              AR Zeitung Demo
            </h6>
            <div class="text-subtitlw1">
              {{ todaysDate }}
            </div>
          </q-toolbar-title>

        </q-toolbar>
      </q-item-section>
    </q-item>
    <PageListsScan></PageListsScan>
    <PageListsHelp></PageListsHelp>
    <PageListsContact></PageListsContact>

  </q-drawer>
</template>

<script>

import { defineComponent, ref } from 'vue';
import Scan from './Scan.vue';

import PageListsScan from 'src/components/pagelists/PageListsScan.vue'
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

    PageListsScan,
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

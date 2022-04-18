<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar class="bg-dark">
        <q-btn
          class="z-top q-ma-sm"
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="toggleLeftDrawer"
        />
        <img
          src="https://holonative.de/wp-content/uploads/2020/06/holonative_transparent_500px_167px.png"
          alt="holologo"
          height="40"
        >
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
      class="bg-indigo-1 z-top"
    >

      <q-item class="bg-dark text-white">
        <q-item-section>
          <q-toolbar>

            <q-toolbar-title>
              <img
                src="https://holonative.de/wp-content/uploads/2020/06/holonative_transparent_500px_167px.png"
                alt="holologo"
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
    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>


import { defineComponent, ref } from 'vue'
import PageListsHelp from 'src/components/pagelists/PageListsHelp.vue'
import PageListsContact from 'src/components/pagelists/PageListsContact.vue'

export default defineComponent({
  name: 'MainLayout',

  components: {
    PageListsHelp,
    PageListsContact
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
})
</script>

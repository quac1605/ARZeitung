<template>
  <q-layout view="lHh Lpr lFf">

    <!-- <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
    >

      <q-item class="bg-grey-3">
        <q-item-section>
          Pages
        </q-item-section>
      </q-item>
      <PageListsScan></PageListsScan>
      <PageListsHelp></PageListsHelp>
      <PageListsContact></PageListsContact>

    </q-drawer> -->
    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>


import { defineComponent, ref } from 'vue'
//import { date } from 'quasar'

// import PageListsScan from 'src/components/pagelists/PageListsScan.vue'
// import PageListsHelp from 'src/components/pagelists/PageListsHelp.vue'
// import PageListsContact from 'src/components/pagelists/PageListsContact.vue'

export default defineComponent({
  name: 'MainLayout',

  components: {
    // PageListsScan,
    // PageListsHelp,
    // PageListsContact
  },

  // setup () {
  //   const leftDrawerOpen = ref(false)

  //   return {

  //     leftDrawerOpen,
  //     toggleLeftDrawer () {
  //       leftDrawerOpen.value = !leftDrawerOpen.value
  //     }
  //   }
  // },
  // computed: {
  //   todaysDate () {
  //     const timeStamp = Date.now()
  //     return date.formatDate(timeStamp, 'dddd D MMMM')
  //   }
  // }
})
</script>

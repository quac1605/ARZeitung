<template>
  <q-list>
    <q-item
      clickable
      v-ripple
      @click="handleButtonClick"
    >
      <q-item-section side>
        <q-icon
          name="mdi-contacts-outline"
          size="sm"
        />
      </q-item-section>
      <q-item-section class="text-gray-9">
        Contact
      </q-item-section>
    </q-item>
    <q-dialog
      v-model="prompt"
      persistent
    >
      <q-card style="min-width: 350px">

        <q-card-actions
          align="center"
          class="text-primary"
        >

          <q-card-section>
            <div><img
                src="https://holonative.de/wp-content/uploads/2022/03/A6501084-1280x1707.jpg"
                width="200"
                height="300"
              ></div>
          </q-card-section>
          <q-card-section>
            <div>
              <q-btn
                round
                color="dark"
                href="https://www.facebook.com/nhatquang998"
              ><i class="fa-brands fa-facebook-f fa-xl"></i></q-btn>
            </div>
          </q-card-section>

        </q-card-actions>
        <q-card-actions
          align="right"
          class="text-primary"
        >
          <q-btn
            v-close-popup
            flat
            label="Cancel"
          />
        </q-card-actions>
      </q-card>
    </q-dialog>
  </q-list>
</template>

<script>
export default {
  // name: 'ComponentName',
  setup () {
    return {}
  },
  // inject: ['setSelectedTab'],
  methods: {
    handleButtonClick () {
      this.prompt = !this.prompt
    },
  },
  data () {
    return {
      prompt: false,

    }
  },
}
</script>


<template>
  <q-list bordered>
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
      class="dialog"
    >
      <q-card
        style="min-width: 350px"
        class="bg-grey-4"
      >

        <q-card-actions
          align="center"
          class="text-primary"
        >

          <q-card-section>
            <div><a href="https://holonative.de/ueber-uns/"><img
                  src="https://holonative.de/wp-content/uploads/2020/06/holoNative_1000px_333px.png"
                  width="250"
                  height="100"
                ></a></div>
          </q-card-section>
          <q-card-section>
            <span
              style="font-size: 16px"
              class="text-dark"
            >holoNative is a young, creative XR agency from Kiel. In the still new XR industry, we have been able to work with state-of-the-art AR/VR technology in projects, including at state level, since 2017. We design and develop individually meaningful and profitable AR/VR solutions for our customers. For example, we help companies to prepare complex information in a visually understandable way, to add an emotional level to their brand or to enable their customers to interact with the desired product in new ways.</span>
          </q-card-section>

          <q-card-actions align="center">
            <q-card-section>
              <div>
                <q-btn
                  round
                  color="grey"
                  href="https://www.facebook.com/holonative.de"
                ><i class="fa-brands fa-facebook-f fa-xl"></i></q-btn>
              </div>
            </q-card-section>
            <q-card-section>
              <div>
                <q-btn
                  round
                  color="grey"
                  href="https://www.linkedin.com/company/holonative/"
                ><i class="fa-brands fa-linkedin-in fa-xl"></i></q-btn>
              </div>
            </q-card-section>
            <q-card-section>
              <div>
                <q-btn
                  round
                  color="grey"
                  href="https://www.instagram.com/holonatives/"
                ><i class="fa-brands fa-instagram fa-xl"></i></q-btn>
              </div>
            </q-card-section>
          </q-card-actions>
        </q-card-actions>
        <q-card-actions align="right">
          <q-btn
            push
            rounded
            v-close-popup
            label="Cancel"
            class="bg-grey-9 text-white"
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



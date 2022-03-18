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
            >holoNative ist eine junge, kreative XR-Agentur aus Kiel. In der noch neuen XR-Industrie konnten wir bereits seit 2017 in Projekten, u.a. auf Landesebene, mit modernster AR/VR-Technologie arbeiten. Wir konzipieren und entwickeln für unsere Kundschaft individuell sinnvolle und profitable AR/VR-Lösungen. So helfen wir Unternehmen beispielsweise komplexe Informationen verständlich visuell aufzubereiten, ihre Marke um eine emotionale Ebene zu erweitern oder ihrer Kundschaft neue Interaktionsmöglichkeiten mit dem gewünschten Produkt zu ermöglichen.</span>
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



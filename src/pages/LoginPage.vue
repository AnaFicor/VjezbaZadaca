
<template>
  <q-page class="q-pa-md">
    <div class="text-h3 text-center q-mb-md">Prijava</div>

    <div class="text-h6 text-center q-mb-lg">
      Prijavite se svojim korisničkim podacima.
    </div>

    <div class="row justify-center">
      <div class="col-12 col-md-6">
        <q-input
          outlined
          v-model="korisnickoIme"
          label="Korisničko ime"
          class="q-mb-md"
        />

        <q-input
          outlined
          v-model="lozinka"
          label="Lozinka"
          type="password"
          class="q-mb-md"
        />

        <div class="text-center">
          <q-btn color="primary" label="Potvrdi" @click="potvrdi" />
        </div>
      </div>
    </div>
  </q-page>
</template>

<script>
import { ref } from 'vue'

export default {
  setup () {
    const korisnickoIme = ref('')
    const lozinka = ref('')

    function potvrdi () {
      console.log('Korisničko ime:', korisnickoIme.value)
    }

    return {
      korisnickoIme,
      lozinka,
      potvrdi
    }
  }
}
</script>

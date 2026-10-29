
<template>
  <q-page class="q-pa-md">
    <div class="text-h3 text-center q-mb-md">Registracija</div>

    <div class="text-h6 text-center q-mb-lg">
      Ispunite podatke za registraciju u knjižnicu.
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
          v-model="ime"
          label="Ime"
          class="q-mb-md"
        />

        <q-input
          outlined
          v-model="prezime"
          label="Prezime"
          class="q-mb-md"
        />

        <q-input
          outlined
          v-model="email"
          label="E-mail"
          type="email"
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
    const ime = ref('')
    const prezime = ref('')
    const email = ref('')
    const lozinka = ref('')

    function potvrdi () {
      console.log('Podaci za registraciju:', {
        korisnickoIme: korisnickoIme.value,
        ime: ime.value,
        prezime: prezime.value,
        email: email.value
      })
    }

    return {
      korisnickoIme,
      ime,
      prezime,
      email,
      lozinka,
      potvrdi
    }
  }
}
</script>

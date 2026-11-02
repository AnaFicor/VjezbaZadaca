
<template>
  <q-page class="register-page flex flex-center q-pa-md">

    <div class="register-container">

      <div class="text-center q-mb-lg">
        <div class="register-logo">
          <q-icon name="person_add" size="42px" />
        </div>

        <div class="register-title q-mt-md">
          Postani član naše knjižnice
        </div>

        <div class="register-subtitle">
          Kreirajte svoj korisnički račun i otkrijte svijet knjiga.
        </div>
      </div>

      <q-card class="register-card">
        <q-card-section class="q-pa-lg">

          <div class="card-title q-mb-xs">
            <q-icon name="person_add" color="purple-4" size="25px" />
            Registracija korisnika
          </div>

          <div class="card-subtitle q-mb-lg">
            Ispunite sva polja za kreiranje računa.
          </div>

          <div class="input-label">KORISNIČKO IME</div>
          <q-input
            v-model="korisnickoIme"
            outlined
            placeholder="Odaberite korisničko ime"
            class="register-input q-mb-md"
          >
            <template v-slot:prepend>
              <q-icon name="person" color="purple-5" />
            </template>
          </q-input>

          <div class="input-label">IME</div>
          <q-input
            v-model="ime"
            outlined
            placeholder="Unesite ime"
            class="register-input q-mb-md"
          >
            <template v-slot:prepend>
              <q-icon name="badge" color="purple-5" />
            </template>
          </q-input>

          <div class="input-label">PREZIME</div>
          <q-input
            v-model="prezime"
            outlined
            placeholder="Unesite prezime"
            class="register-input q-mb-md"
          >
            <template v-slot:prepend>
              <q-icon name="badge" color="purple-5" />
            </template>
          </q-input>

          <div class="input-label">E-MAIL ADRESA</div>
          <q-input
            v-model="email"
            outlined
            type="email"
            placeholder="primjer@email.com"
            class="register-input q-mb-md"
          >
            <template v-slot:prepend>
              <q-icon name="mail" color="purple-5" />
            </template>
          </q-input>

          <div class="input-label">LOZINKA</div>
          <q-input
            v-model="lozinka"
            outlined
            :type="prikaziLozinku ? 'text' : 'password'"
            placeholder="Odaberite lozinku"
            class="register-input q-mb-md"
          >
            <template v-slot:prepend>
              <q-icon name="lock" color="purple-5" />
            </template>

            <template v-slot:append>
              <q-icon
                :name="prikaziLozinku ? 'visibility_off' : 'visibility'"
                class="cursor-pointer"
                color="purple-5"
                @click="prikaziLozinku = !prikaziLozinku"
              />
            </template>
          </q-input>

          <q-banner
            v-if="poruka"
            rounded
            class="q-mb-md"
            :class="uspjeh ? 'success-message' : 'error-message'"
          >
            <template v-slot:avatar>
              <q-icon :name="uspjeh ? 'check_circle' : 'error'" />
            </template>
            {{ poruka }}
          </q-banner>

          <q-btn
            unelevated
            label="KREIRAJ RAČUN"
            icon-right="arrow_forward"
            class="register-button full-width q-mt-sm"
            @click="potvrdi"
          />

          <q-separator class="q-my-lg register-separator" />

          <div class="text-center login-text">
            Već imate račun?

            <router-link to="/login" class="login-link">
              Prijavite se
            </router-link>
          </div>

        </q-card-section>
      </q-card>

      <div class="bottom-text text-center q-mt-lg">
        <q-icon name="favorite" color="purple-4" />
        Vaša nova čitateljska avantura počinje ovdje.
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
    const prikaziLozinku = ref(false)

    const poruka = ref('')
    const uspjeh = ref(false)

    function potvrdi () {
      poruka.value = ''
      uspjeh.value = false

      if (
        !korisnickoIme.value.trim() ||
        !ime.value.trim() ||
        !prezime.value.trim() ||
        !email.value.trim() ||
        !lozinka.value
      ) {
        poruka.value = 'Molimo ispunite sva polja.'
        return
      }

      const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/

      if (!emailRegex.test(email.value)) {
        poruka.value = 'Unesite ispravnu e-mail adresu.'
        return
      }

      if (lozinka.value.length < 6) {
        poruka.value = 'Lozinka mora imati najmanje 6 znakova.'
        return
      }

      console.log('Podaci za registraciju:', {
        korisnickoIme: korisnickoIme.value,
        ime: ime.value,
        prezime: prezime.value,
        email: email.value
      })

      uspjeh.value = true
      poruka.value = 'Podaci su uspješno uneseni! Registracija još nije povezana s bazom podataka.'
    }

    return {
      korisnickoIme,
      ime,
      prezime,
      email,
      lozinka,
      prikaziLozinku,
      poruka,
      uspjeh,
      potvrdi
    }
  }
}
</script>

<style scoped>
.register-page {
  min-height: calc(100vh - 75px);
  background: transparent;
}

.register-container {
  width: 100%;
  max-width: 480px;
}

.register-logo {
  width: 78px;
  height: 78px;
  margin: auto;
  display: flex;
  justify-content: center;
  align-items: center;
  color: #e3c5ff;
  background: linear-gradient(135deg, #7835a5, #35164c);
  border-radius: 23px;
  box-shadow: 0 8px 25px rgba(147, 70, 194, 0.3);
}

.register-title {
  font-size: 27px;
  font-weight: bold;
  color: #f2e6ff;
}

.register-subtitle {
  color: #a995ba;
  font-size: 13px;
  margin-top: 8px;
}

.register-card {
  background: #191221;
  border: 1px solid #49305d;
  border-radius: 20px;
  box-shadow: 0 12px 40px rgba(0, 0, 0, 0.35);
}

.card-title {
  display: flex;
  align-items: center;
  gap: 10px;
  font-size: 20px;
  font-weight: bold;
  color: #f0e2ff;
}

.card-subtitle {
  color: #9f8aaf;
  font-size: 13px;
}

.input-label {
  color: #bd96df;
  font-size: 11px;
  font-weight: bold;
  letter-spacing: 1.5px;
  margin-bottom: 8px;
}

.register-input :deep(.q-field__control) {
  background: #24192f;
  border-radius: 11px;
  height: 52px;
}

.register-input :deep(.q-field__control:before) {
  border-color: #634278;
}

.register-input :deep(.q-field__control:hover:before) {
  border-color: #a66bce;
}

.register-input :deep(.q-field__control:after) {
  border-color: #bc86e8;
}

.register-input :deep(.q-field__native) {
  color: #ffffff !important;
}

.register-input :deep(.q-field__native::placeholder) {
  color: #aa98b8 !important;
  opacity: 1;
}

.register-button {
  height: 50px;
  border-radius: 11px;
  background: linear-gradient(90deg, #7536a2, #a14dcc);
  color: white;
  font-weight: bold;
  letter-spacing: 1px;
  transition: 0.3s;
}

.register-button:hover {
  background: linear-gradient(90deg, #9149c0, #bd70e5);
  box-shadow: 0 5px 20px rgba(164, 78, 211, 0.3);
}

.error-message {
  background: #3a1d2a;
  color: #ffb3c1;
}

.success-message {
  background: #20372b;
  color: #a7e9bd;
}

.register-separator {
  background: #392747;
}

.login-text {
  color: #a895b7;
  font-size: 13px;
}

.login-link {
  color: #c18aef;
  font-weight: bold;
  text-decoration: none;
  margin-left: 4px;
}

.login-link:hover {
  color: #e0baff;
  text-decoration: underline;
}

.bottom-text {
  color: #9581a6;
  font-size: 12px;
}

.bottom-text .q-icon {
  margin-right: 5px;
}

@media (max-width: 500px) {
  .register-title {
    font-size: 23px;
  }

  .register-card {
    border-radius: 15px;
  }
}
</style>

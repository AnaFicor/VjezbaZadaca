
<template>
  <q-page class="login-page flex flex-center q-pa-md">

    <div class="login-container">

      <div class="text-center q-mb-lg">
        <div class="login-logo">
          <q-icon name="auto_stories" size="45px" />
        </div>

        <div class="login-title q-mt-md">
          Dobrodošli natrag!
        </div>

        <div class="login-subtitle">
          Prijavite se u svoju digitalnu knjižnicu.
        </div>
      </div>

      <q-card class="login-card">
        <q-card-section class="q-pa-lg">

          <div class="card-title q-mb-xs">
            <q-icon name="login" color="purple-4" size="25px" />
            Prijava korisnika
          </div>

          <div class="card-subtitle q-mb-lg">
            Unesite svoje podatke za nastavak.
          </div>

          <div class="input-label">KORISNIČKO IME</div>

          <q-input
            v-model="korisnickoIme"
            outlined
            placeholder="Unesite korisničko ime"
            class="login-input q-mb-lg"
            @keyup.enter="potvrdi"
          >
            <template v-slot:prepend>
              <q-icon name="person" color="purple-5" />
            </template>
          </q-input>

          <div class="input-label">LOZINKA</div>

          <q-input
            v-model="lozinka"
            outlined
            placeholder="Unesite lozinku"
            :type="prikaziLozinku ? 'text' : 'password'"
            class="login-input q-mb-md"
            @keyup.enter="potvrdi"
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
            label="PRIJAVI SE"
            icon-right="arrow_forward"
            class="login-button full-width q-mt-sm"
            @click="potvrdi"
          />

          <q-separator class="q-my-lg login-separator" />

          <div class="text-center register-text">
            Nemate korisnički račun?

            <router-link to="/registracija" class="register-link">
              Registrirajte se
            </router-link>
          </div>

        </q-card-section>
      </q-card>

      <div class="bottom-text text-center q-mt-lg">
        <q-icon name="favorite" color="purple-4" />
        Vaše mjesto za ljubav prema knjigama.
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
    const prikaziLozinku = ref(false)

    const poruka = ref('')
    const uspjeh = ref(false)

    function potvrdi () {
      poruka.value = ''
      uspjeh.value = false

      if (!korisnickoIme.value.trim() || !lozinka.value) {
        poruka.value = 'Molimo unesite korisničko ime i lozinku.'
        return
      }

      console.log('Korisničko ime:', korisnickoIme.value)

      poruka.value = 'Podaci su uneseni! Prijava još nije povezana s bazom korisnika.'
    }

    return {
      korisnickoIme,
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
.login-page {
  min-height: calc(100vh - 75px);
  background: transparent;
}

.login-container {
  width: 100%;
  max-width: 460px;
}

.login-logo {
  width: 85px;
  height: 85px;
  margin: auto;
  display: flex;
  justify-content: center;
  align-items: center;
  color: #e0baff;
  background: linear-gradient(135deg, #7835a5, #35164c);
  border-radius: 25px;
  box-shadow: 0 8px 30px rgba(147, 70, 194, 0.3);
}

.login-title {
  font-size: 29px;
  font-weight: bold;
  color: #f2e6ff;
}

.login-subtitle {
  color: #a995ba;
  font-size: 13px;
  margin-top: 8px;
}

.login-card {
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
  margin-bottom: 9px;
}

.login-input :deep(.q-field__control) {
  background: #24192f;
  border-radius: 11px;
  height: 52px;
}

.login-input :deep(.q-field__control:before) {
  border-color: #634278;
}

.login-input :deep(.q-field__control:hover:before) {
  border-color: #a66bce;
}

.login-input :deep(.q-field__control:after) {
  border-color: #bc86e8;
}

.login-input :deep(.q-field__native) {
  color: #ffffff !important;
}

.login-input :deep(.q-field__native::placeholder) {
  color: #aa98b8 !important;
  opacity: 1;
}

.login-button {
  height: 50px;
  border-radius: 11px;
  background: linear-gradient(90deg, #7536a2, #a14dcc);
  color: white;
  font-weight: bold;
  letter-spacing: 1px;
  transition: 0.3s;
}

.login-button:hover {
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

.login-separator {
  background: #392747;
}

.register-text {
  color: #a895b7;
  font-size: 13px;
}

.register-link {
  color: #c18aef;
  font-weight: bold;
  text-decoration: none;
  margin-left: 4px;
}

.register-link:hover {
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
  .login-title {
    font-size: 25px;
  }

  .login-card {
    border-radius: 15px;
  }

  .login-logo {
    width: 70px;
    height: 70px;
  }
}
</style>


<template>
  <q-page class="location-page q-pa-lg">

    <div class="page-heading">
      <div class="heading-icon">
        <q-icon name="location_on" size="38px" />
      </div>

      <div>
        <div class="page-title">Gdje se nalazimo?</div>
        <div class="page-subtitle">
          Posjetite Gradsku knjižnicu Rijeka.
        </div>
      </div>
    </div>

    <q-card class="location-card">

      <q-card-section class="location-info">
        <div class="info-icon">
          <q-icon name="account_balance" size="30px" />
        </div>

        <div class="info-content">
          <div class="info-title">Gradska knjižnica Rijeka</div>
          <div class="info-description">
            Pronađite nas i posjetite našu knjižnicu.
          </div>
        </div>

        <q-btn
          unelevated
          icon="directions"
          label="Upute za dolazak"
          class="directions-button"
          type="a"
          href="https://www.google.com/maps/dir/?api=1&destination=45.3312,14.4322"
          target="_blank"
        />
      </q-card-section>

      <q-separator color="purple-10" />

      <q-card-section class="q-pa-md">
        <div id="map" class="map-container"></div>
      </q-card-section>

      <q-card-section class="address-section">
        <q-icon name="place" color="purple-4" size="25px" />
        <div>
          <div class="address-title">Naša lokacija</div>
          <div class="address-description">
            Gradska knjižnica Rijeka, Rijeka, Hrvatska
          </div>
        </div>
      </q-card-section>

    </q-card>

    <div class="bottom-text">
      <q-icon name="favorite" color="purple-4" />
      Veselimo se vašem dolasku!
    </div>

  </q-page>
</template>

<script>
import { ref, onMounted, onBeforeUnmount, nextTick } from 'vue'
import * as L from 'leaflet'
import 'leaflet/dist/leaflet.css'

import markerIcon from 'leaflet/dist/images/marker-icon.png'
import markerShadow from 'leaflet/dist/images/marker-shadow.png'

export default {
  setup () {
    const initialMap = ref(null)

    onMounted(async () => {
      await nextTick()

      const icon = L.icon({
        iconUrl: markerIcon,
        shadowUrl: markerShadow,
        iconSize: [25, 41],
        iconAnchor: [12, 41],
        popupAnchor: [1, -34],
        shadowSize: [41, 41]
      })

      initialMap.value = L.map('map').setView(
        [45.3312, 14.4322],
        16
      )

      L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
        maxZoom: 19,
        attribution: '&copy; OpenStreetMap'
      }).addTo(initialMap.value)

      L.marker([45.3312, 14.4322], { icon })
        .addTo(initialMap.value)
        .bindPopup('<b>Gradska knjižnica Rijeka</b><br>Dobrodošli!')
        .openPopup()

      setTimeout(() => {
        initialMap.value?.invalidateSize()
      }, 200)
    })

    onBeforeUnmount(() => {
      if (initialMap.value) {
        initialMap.value.remove()
        initialMap.value = null
      }
    })

    return {
      initialMap
    }
  }
}
</script>

<style scoped>
.location-page {
  min-height: 100vh;
  color: #f5efff;
}

.page-heading {
  display: flex;
  align-items: center;
  gap: 20px;
  margin: 15px 0 30px;
}

.heading-icon {
  width: 75px;
  height: 75px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 20px;
  color: #d1a5ff;
  background: linear-gradient(135deg, #682b91, #321744);
}

.page-title {
  font-size: 30px;
  font-weight: bold;
  color: #f4eaff;
}

.page-subtitle {
  color: #a997b8;
  font-size: 14px;
  margin-top: 6px;
}

.location-card {
  background: #191221;
  border: 1px solid #49305d;
  border-radius: 18px;
  overflow: hidden;
  box-shadow: 0 8px 30px rgba(0, 0, 0, 0.25);
}

.location-info {
  display: flex;
  align-items: center;
  gap: 15px;
  padding: 22px;
}

.info-icon {
  width: 55px;
  height: 55px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: #d1a5ff;
  background: #38204b;
  border-radius: 14px;
}

.info-content {
  flex: 1;
}

.info-title {
  font-size: 17px;
  font-weight: bold;
  color: #f0e2ff;
}

.info-description {
  font-size: 12px;
  color: #a997b8;
  margin-top: 4px;
}

.directions-button {
  background: linear-gradient(90deg, #7536a2, #a14dcc);
  color: white;
  border-radius: 9px;
  font-size: 12px;
}

.map-container {
  height: 480px;
  width: 100%;
  border-radius: 12px;
  overflow: hidden;
  z-index: 1;
}

.address-section {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 20px 25px;
}

.address-title {
  color: #e5d2f5;
  font-weight: bold;
  font-size: 14px;
}

.address-description {
  color: #a997b8;
  font-size: 12px;
  margin-top: 4px;
}

.bottom-text {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 8px;
  color: #9581a6;
  font-size: 12px;
  margin-top: 25px;
}

@media (max-width: 600px) {
  .page-title {
    font-size: 23px;
  }

  .heading-icon {
    width: 58px;
    height: 58px;
  }

  .location-info {
    flex-wrap: wrap;
  }

  .directions-button {
    width: 100%;
  }

  .map-container {
    height: 350px;
  }
}
</style>

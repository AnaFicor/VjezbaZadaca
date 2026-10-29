
<template>
  <q-page class="q-pa-md">
    <div class="text-h3 text-center q-mb-md">
      Gdje se nalazimo?
    </div>

    <div class="text-h6 text-center q-mb-lg">
      Posjetite Gradsku knjižnicu Rijeka. Na karti možete pronaći našu lokaciju.
    </div>

    <div id="map" style="height:500px;"></div>
  </q-page>
</template>

<script>
import { ref, onMounted } from 'vue'
import * as L from 'leaflet'
import 'leaflet/dist/leaflet.css'

export default {
  setup () {
    const initialMap = ref('')

    onMounted(() => {
      initialMap.value = L.map('map').setView([45.3312, 14.4322], 13)

      L.tileLayer('https://tile.openstreetmap.org/{z}/{x}/{y}.png', {
        maxZoom: 19,
        attribution: '&copy;<a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a>'
      }).addTo(initialMap.value)
    })

    return {
      initialMap
    }
  }
}
</script>

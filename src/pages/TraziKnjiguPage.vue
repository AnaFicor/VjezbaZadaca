
<template>
  <q-page class="q-pa-md">
    <div class="text-h3 text-center q-mb-md">Pretraživanje knjiga</div>

    <div class="text-h6 text-center q-mb-lg">
      Pronađite knjigu prema njezinu naslovu ili autoru.
    </div>

    <div class="row q-col-gutter-md items-center">
      <div class="col-12 col-md-6">
        <q-input
          outlined
          v-model="pojam"
          label="Unesite naslov ili autora"
        />
      </div>

      <div class="col-12 col-md-3">
        <q-checkbox v-model="poNaslovu" label="Pretraži po naslovu" />
      </div>

      <div class="col-12 col-md-3">
        <q-checkbox v-model="poAutoru" label="Pretraži po autoru" />
      </div>
    </div>

    <div class="text-center q-mt-md q-mb-lg">
      <q-btn color="primary" label="Traži" @click="trazi" />
    </div>

    <q-table
      title="Rezultati pretraživanja"
      :rows="rezultati"
      :columns="columns"
      row-key="id"
    />
  </q-page>
</template>

<script>
import { ref } from 'vue'

const columns = [
  {
    name: 'id',
    label: 'ID',
    field: 'id',
    align: 'left',
    sortable: true,
    style: { fontSize: '14px' },
    headerStyle: { fontSize: '18px' }
  },
  {
    name: 'naslov',
    label: 'Naslov',
    field: 'naslov',
    align: 'left',
    sortable: true,
    style: { fontSize: '14px' },
    headerStyle: { fontSize: '18px' }
  },
  {
    name: 'autor',
    label: 'Autor',
    field: 'autor',
    align: 'left',
    sortable: true,
    style: { fontSize: '14px' },
    headerStyle: { fontSize: '18px' }
  }
]

const knjige = [
  { id: 1, naslov: 'Mali princ', autor: 'Antoine de Saint-Exupéry' },
  { id: 2, naslov: 'Zločin i kazna', autor: 'Fjodor Dostojevski' },
  { id: 3, naslov: 'Ponos i predrasude', autor: 'Jane Austen' },
  { id: 4, naslov: '1984.', autor: 'George Orwell' }
]

export default {
  setup () {
    const pojam = ref('')
    const poNaslovu = ref(false)
    const poAutoru = ref(false)
    const rezultati = ref([])

    function trazi () {
      const unos = pojam.value.toLowerCase().trim()

      if (!unos || (!poNaslovu.value && !poAutoru.value)) {
        rezultati.value = []
        return
      }

      rezultati.value = knjige.filter(knjiga => {
        return (
          (poNaslovu.value && knjiga.naslov.toLowerCase().includes(unos)) ||
          (poAutoru.value && knjiga.autor.toLowerCase().includes(unos))
        )
      })
    }

    return {
      columns,
      pojam,
      poNaslovu,
      poAutoru,
      rezultati,
      trazi
    }
  }
}
</script>

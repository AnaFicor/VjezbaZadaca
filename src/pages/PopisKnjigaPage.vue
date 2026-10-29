
<template>
  <q-page class="q-pa-md">
    <div class="text-h3 text-center q-mb-md">Popis svih knjiga</div>
    <div class="text-h6 text-center q-mb-lg">
      Pregledajte popis knjiga dostupnih u našoj knjižnici.
    </div>

    <q-table
      title="Knjige"
      :rows="rows"
      :columns="columns"
      row-key="id"
    />
  </q-page>
</template>

<script>
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
  },
  {
    name: 'godina',
    label: 'Godina izdanja',
    field: 'godina',
    align: 'left',
    sortable: true,
    style: { fontSize: '14px' },
    headerStyle: { fontSize: '18px' }
  }
]

const rows = [
  { id: 1, naslov: 'Mali princ', autor: 'Antoine de Saint-Exupéry', godina: 1943 },
  { id: 2, naslov: 'Zločin i kazna', autor: 'Fjodor Dostojevski', godina: 1866 },
  { id: 3, naslov: 'Ponos i predrasude', autor: 'Jane Austen', godina: 1813 },
  { id: 4, naslov: '1984.', autor: 'George Orwell', godina: 1949 }
]

export default {
  setup () {
    return {
      columns,
      rows
    }
  }
}
</script>

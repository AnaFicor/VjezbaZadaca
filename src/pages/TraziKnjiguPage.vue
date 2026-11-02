
<template>
  <q-page class="search-page q-pa-lg">

    <div class="page-heading">
      <div class="heading-icon">
        <q-icon name="search" size="38px" />
      </div>

      <div>
        <div class="page-title">Pretraživanje knjiga</div>
        <div class="page-subtitle">
          Pronađite svoju sljedeću omiljenu knjigu.
        </div>
      </div>
    </div>

    <q-card class="search-card">

      <q-card-section class="q-pa-lg">

        <div class="section-title">
          <q-icon name="manage_search" color="purple-4" size="27px" />
          Pronađite knjigu
        </div>

        <div class="search-description">
          Unesite naslov ili ime autora i odaberite način pretraživanja.
        </div>

        <q-input
          v-model="pojam"
          outlined
          clearable
          placeholder="Unesite naslov ili autora..."
          class="search-input q-mt-lg"
          @keyup.enter="trazi"
        >
          <template v-slot:prepend>
            <q-icon name="search" color="purple-4" />
          </template>
        </q-input>

        <div class="checkbox-area q-mt-md">
          <q-checkbox
            v-model="poNaslovu"
            label="Pretraži po naslovu"
            color="purple-5"
          />

          <q-checkbox
            v-model="poAutoru"
            label="Pretraži po autoru"
            color="purple-5"
          />
        </div>

        <div class="row q-col-gutter-sm q-mt-md">
          <div class="col-12 col-sm-6">
            <q-btn
              unelevated
              icon="search"
              label="TRAŽI"
              class="search-button full-width"
              @click="trazi"
            />
          </div>

          <div class="col-12 col-sm-6">
            <q-btn
              outline
              icon="refresh"
              label="OČISTI"
              class="clear-button full-width"
              @click="ocisti"
            />
          </div>
        </div>

        <q-banner
          v-if="poruka"
          rounded
          class="q-mt-md search-message"
        >
          <template v-slot:avatar>
            <q-icon name="info" color="purple-3" />
          </template>
          {{ poruka }}
        </q-banner>

      </q-card-section>
    </q-card>

    <q-card class="results-card q-mt-lg">

      <q-card-section class="results-heading">
        <div>
          <div class="results-title">
            <q-icon name="library_books" color="purple-4" size="25px" />
            Rezultati pretraživanja
          </div>

          <div class="results-subtitle">
            Pronađene knjige u našoj knjižnici
          </div>
        </div>

        <div class="results-count">
          {{ rezultati.length }} knjiga
        </div>
      </q-card-section>

      <q-separator color="purple-10" />

      <q-table
        :rows="rezultati"
        :columns="columns"
        row-key="id"
        flat
        :pagination="pagination"
        no-data-label="Nema pronađenih knjiga."
        class="results-table"
      >

        <template v-slot:body-cell-id="props">
          <q-td :props="props">
            <span class="id-badge">#{{ props.value }}</span>
          </q-td>
        </template>

        <template v-slot:body-cell-naslov="props">
          <q-td :props="props">
            <div class="book-title">
              <q-icon
                name="menu_book"
                color="purple-4"
                size="20px"
                class="q-mr-sm"
              />
              {{ props.value }}
            </div>
          </q-td>
        </template>

      </q-table>

    </q-card>

    <div class="bottom-text">
      <q-icon name="favorite" color="purple-4" />
      Pronađite priču koja će vas inspirirati.
    </div>

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
    sortable: true
  },
  {
    name: 'naslov',
    label: 'NASLOV KNJIGE',
    field: 'naslov',
    align: 'left',
    sortable: true
  },
  {
    name: 'autor',
    label: 'AUTOR',
    field: 'autor',
    align: 'left',
    sortable: true
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
    const poNaslovu = ref(true)
    const poAutoru = ref(true)
    const rezultati = ref([])
    const poruka = ref('')

    const pagination = ref({
      rowsPerPage: 10
    })

    function trazi () {
      const unos = pojam.value.trim().toLocaleLowerCase('hr')

      poruka.value = ''

      if (!unos) {
        rezultati.value = []
        poruka.value = 'Unesite naslov ili autora koji želite pronaći.'
        return
      }

      if (!poNaslovu.value && !poAutoru.value) {
        rezultati.value = []
        poruka.value = 'Odaberite barem jedan način pretraživanja.'
        return
      }

      rezultati.value = knjige.filter(knjiga => {
        const naslov = knjiga.naslov.toLocaleLowerCase('hr')
        const autor = knjiga.autor.toLocaleLowerCase('hr')

        return (
          (poNaslovu.value && naslov.includes(unos)) ||
          (poAutoru.value && autor.includes(unos))
        )
      })

      if (rezultati.value.length === 0) {
        poruka.value = 'Nažalost, nema knjiga koje odgovaraju vašoj pretrazi.'
      } else {
        poruka.value = `Pronađeno knjiga: ${rezultati.value.length}.`
      }
    }

    function ocisti () {
      pojam.value = ''
      poNaslovu.value = true
      poAutoru.value = true
      rezultati.value = []
      poruka.value = ''
    }

    return {
      columns,
      pojam,
      poNaslovu,
      poAutoru,
      rezultati,
      poruka,
      pagination,
      trazi,
      ocisti
    }
  }
}
</script>

<style scoped>
.search-page {
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

.search-card,
.results-card {
  background: #191221;
  border: 1px solid #49305d;
  border-radius: 18px;
  box-shadow: 0 8px 30px rgba(0, 0, 0, 0.2);
  overflow: hidden;
}

.section-title,
.results-title {
  display: flex;
  align-items: center;
  gap: 10px;
  color: #f0e2ff;
  font-size: 20px;
  font-weight: bold;
}

.search-description,
.results-subtitle {
  color: #a997b8;
  font-size: 13px;
  margin-top: 7px;
}

.search-input :deep(.q-field__control) {
  background: #24192f;
  border-radius: 11px;
  min-height: 52px;
}

.search-input :deep(.q-field__control:before) {
  border-color: #634278;
}

.search-input :deep(.q-field__control:hover:before) {
  border-color: #a66bce;
}

.search-input :deep(.q-field__control:after) {
  border-color: #bc86e8;
}

.search-input :deep(.q-field__native) {
  color: white !important;
}

.search-input :deep(.q-field__native::placeholder) {
  color: #aa98b8 !important;
  opacity: 1;
}

.checkbox-area {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  color: #dfc9f2;
}

.checkbox-area :deep(.q-checkbox__label) {
  font-size: 13px;
}

.search-button {
  height: 48px;
  border-radius: 10px;
  background: linear-gradient(90deg, #7536a2, #a14dcc);
  color: white;
  font-weight: bold;
  letter-spacing: 1px;
}

.clear-button {
  height: 48px;
  border-radius: 10px;
  color: #c69aff;
  border-color: #70468d;
  font-weight: bold;
}

.search-message {
  background: #2b1c39;
  color: #dfc6f5;
  font-size: 13px;
}

.results-heading {
  padding: 22px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 12px;
}

.results-count {
  color: #dfbdff;
  background: #46245f;
  padding: 8px 13px;
  border-radius: 9px;
  font-size: 12px;
  font-weight: bold;
  white-space: nowrap;
}

.results-table {
  background: #191221;
  color: #e9ddf4;
}

.results-table :deep(thead tr th) {
  background: #281936;
  color: #c9a0eb;
  font-size: 12px;
  font-weight: bold;
  letter-spacing: 1px;
  padding: 16px;
}

.results-table :deep(tbody td) {
  padding: 16px;
  font-size: 14px;
  border-color: #30223c;
}

.results-table :deep(tbody tr:hover) {
  background: #30203f;
}

.id-badge {
  background: #46245f;
  color: #dfbdff;
  padding: 6px 12px;
  border-radius: 8px;
  font-size: 12px;
  font-weight: bold;
}

.book-title {
  display: flex;
  align-items: center;
  color: #f0e3ff;
  font-weight: 600;
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

  .checkbox-area {
    flex-direction: column;
    gap: 5px;
  }

  .results-heading {
    align-items: flex-start;
    flex-direction: column;
  }
}
</style>

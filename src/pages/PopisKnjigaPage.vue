
<template>
  <q-page class="q-pa-lg books-page">

    <div class="page-heading">
      <div class="heading-icon">
        <q-icon name="auto_stories" size="38px" />
      </div>

      <div>
        <div class="text-h4 text-weight-bold heading-title">
          Popis svih knjiga
        </div>

        <div class="heading-subtitle">
          Otkrijte zanimljive naslove iz naše knjižnice.
        </div>
      </div>
    </div>

    <div class="stats-card q-mt-lg q-mb-lg">
      <div class="stats-icon">
        <q-icon name="menu_book" size="30px" />
      </div>

      <div>
        <div class="stats-number">{{ rows.length }}</div>
        <div class="stats-label">Ukupno knjiga u knjižnici</div>
      </div>
    </div>

    <q-card class="books-card">

      <q-card-section class="table-heading">
        <div>
          <div class="text-h6 text-weight-bold">
            <q-icon name="library_books" color="purple-4" size="25px" />
            Dostupne knjige
          </div>

          <div class="table-subtitle">
            Pregled svih knjiga u našoj kolekciji
          </div>
        </div>
      </q-card-section>

      <q-separator color="purple-10" />

      <q-card-section>
        <q-input
          v-model="filter"
          outlined
          dense
          dark
          clearable
          placeholder="Pretraži naslov, autora ili godinu..."
          class="search-input"
        >
          <template v-slot:prepend>
            <q-icon name="search" color="purple-4" />
          </template>
        </q-input>
      </q-card-section>

      <q-table
        :rows="rows"
        :columns="columns"
        :filter="filter"
        row-key="id"
        flat
        dark
        :pagination="pagination"
        no-data-label="Nema pronađenih knjiga."
        class="books-table"
      >

        <template v-slot:body-cell-id="props">
          <q-td :props="props">
            <span class="id-badge">
              #{{ props.value }}
            </span>
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

        <template v-slot:body-cell-godina="props">
          <q-td :props="props">
            <span class="year-badge">
              {{ props.value }}
            </span>
          </q-td>
        </template>

      </q-table>

    </q-card>

    <div class="bottom-text">
      <q-icon name="favorite" color="purple-4" />
      Svaka knjiga otvara vrata novom svijetu.
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
  },
  {
    name: 'godina',
    label: 'GODINA IZDANJA',
    field: 'godina',
    align: 'left',
    sortable: true
  }
]

const rows = [
  {
    id: 1,
    naslov: 'Mali princ',
    autor: 'Antoine de Saint-Exupéry',
    godina: 1943
  },
  {
    id: 2,
    naslov: 'Zločin i kazna',
    autor: 'Fjodor Dostojevski',
    godina: 1866
  },
  {
    id: 3,
    naslov: 'Ponos i predrasude',
    autor: 'Jane Austen',
    godina: 1813
  },
  {
    id: 4,
    naslov: '1984.',
    autor: 'George Orwell',
    godina: 1949
  }
]

export default {
  setup () {
    const filter = ref('')

    const pagination = ref({
      rowsPerPage: 10,
      sortBy: 'id',
      descending: false
    })

    return {
      columns,
      rows,
      filter,
      pagination
    }
  }
}
</script>

<style scoped>
.books-page {
  min-height: 100vh;
  background: transparent;
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
  box-shadow: 0 5px 20px rgba(126, 54, 177, 0.25);
}

.heading-title {
  color: #f4eaff;
  letter-spacing: 0.5px;
}

.heading-subtitle {
  color: #a997b8;
  font-size: 14px;
  margin-top: 7px;
}

.stats-card {
  display: flex;
  align-items: center;
  gap: 18px;
  width: fit-content;
  min-width: 260px;
  padding: 20px 25px;
  background: linear-gradient(120deg, #281638, #1b1225);
  border: 1px solid #52316b;
  border-radius: 16px;
  box-shadow: 0 5px 20px rgba(0, 0, 0, 0.2);
}

.stats-icon {
  width: 55px;
  height: 55px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 14px;
  color: #d3a5ff;
  background: #472361;
}

.stats-number {
  font-size: 27px;
  font-weight: bold;
  color: #d4a7ff;
}

.stats-label {
  color: #b6a2c7;
  font-size: 12px;
}

.books-card {
  background: #191221;
  border: 1px solid #392747;
  border-radius: 18px;
  overflow: hidden;
  box-shadow: 0 8px 30px rgba(0, 0, 0, 0.25);
}

.table-heading {
  padding: 24px;
}

.table-heading .text-h6 {
  color: #f0e2ff;
  display: flex;
  align-items: center;
  gap: 10px;
}

.table-subtitle {
  color: #9985aa;
  font-size: 12px;
  margin-top: 6px;
}

.search-input {
  max-width: 450px;
}

.search-input :deep(.q-field__control) {
  border-radius: 12px;
  background: #21172d;
}

.search-input :deep(.q-field__native) {
  color: white;
}

.search-input :deep(.q-field__control:before) {
  border-color: #57366f;
}

.search-input :deep(.q-field__control:hover:before) {
  border-color: #a76bd3;
}

.search-input :deep(.q-field__control:after) {
  border-color: #bb83ed;
}


.books-table {
  background: #191221;
  color: #e9ddf4;
}

.books-table :deep(thead tr th) {
  background: #281936;
  color: #c9a0eb;
  font-size: 12px;
  font-weight: bold;
  letter-spacing: 1px;
  padding: 17px 16px;
}

.books-table :deep(tbody td) {
  font-size: 14px;
  padding: 16px;
  border-color: #30223c;
}

.books-table :deep(tbody tr) {
  transition: background 0.2s ease;
}

.books-table :deep(tbody tr:hover) {
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
  font-weight: 600;
  color: #f0e3ff;
}

.year-badge {
  background: #291a36;
  color: #c6a1e4;
  border: 1px solid #503365;
  padding: 6px 11px;
  border-radius: 7px;
  font-size: 12px;
}

.bottom-text {
  text-align: center;
  color: #917da3;
  font-size: 12px;
  margin-top: 30px;
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 8px;
}

@media (max-width: 600px) {
  .books-page {
    padding: 16px !important;
  }

  .heading-title {
    font-size: 25px;
  }

  .heading-icon {
    width: 58px;
    height: 58px;
  }

  .stats-card {
    width: 100%;
  }

  .books-card {
    border-radius: 12px;
  }
}
</style>

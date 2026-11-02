
<template>
  <q-layout view="lHh Lpr lFf" class="library-layout">

    <!-- HEADER -->
    <q-header class="library-header">
      <q-toolbar class="toolbar">

        <q-btn
          flat
          round
          dense
          icon="menu"
          class="menu-btn"
          aria-label="Menu"
          @click="toggleLeftDrawer"
        />

        <div class="brand">
          <q-icon name="auto_stories" size="32px" />
          <q-toolbar-title class="brand-title">
            Knjižnica
            <span class="brand-subtitle">SVIJET KNJIGA</span>
          </q-toolbar-title>
        </div>

        <q-space />

        <div class="header-right">
          <q-icon name="local_library" size="23px" />
          <span>Mjesto za ljubitelje čitanja</span>
        </div>

      </q-toolbar>
    </q-header>

    <!-- SIDEBAR -->
    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
      :width="270"
      class="library-drawer"
    >

      <div class="drawer-content">

        <div class="drawer-logo">
          <div class="logo-icon">
            <q-icon name="menu_book" size="34px" />
          </div>

          <div class="logo-text">
            <div class="logo-title">BOOKSPACE</div>
            <div class="logo-caption">Tvoja digitalna knjižnica</div>
          </div>
        </div>

        <q-separator class="drawer-separator" />

        <div class="menu-heading">GLAVNI IZBORNIK</div>

        <q-list class="navigation-list">

          <EssentialLink
            v-for="link in linksList"
            :key="link.label"
            v-bind="link"
          />

        </q-list>

        <div class="drawer-footer">
          <q-icon name="favorite" color="purple-4" />
          <span>Svaka knjiga krije novu priču.</span>
        </div>

      </div>
    </q-drawer>

    <!-- PAGE CONTENT -->
    <q-page-container class="page-container">
      <router-view />
    </q-page-container>

  </q-layout>
</template>

<script setup>
import { ref } from 'vue'
import EssentialLink from '@/components/EssentialLink.vue'

const linksList = [
  {
    label: 'Naslovnica',
    caption: 'Početna stranica',
    icon: 'home',
    link: '#/'
  },
  {
    label: 'Popis knjiga',
    caption: 'Istraži našu kolekciju',
    icon: 'menu_book',
    link: '#/popis_knjiga'
  },
  {
    label: 'Pretraživanje',
    caption: 'Pronađi svoju knjigu',
    icon: 'search',
    link: '#/pretrazivanje'
  },
  {
    label: 'O nama',
    caption: 'Upoznaj našu knjižnicu',
    icon: 'info',
    link: '#/o_nama'
  },
  {
    label: 'Lokacija',
    caption: 'Pronađi nas',
    icon: 'location_on',
    link: '#/lokacija'
  },
  {
    label: 'Login',
    caption: 'Prijava korisnika',
    icon: 'login',
    link: '#/login'
  },
  {
    label: 'Registracija',
    caption: 'Postani naš član',
    icon: 'person_add',
    link: '#/registracija'
  }
]

const leftDrawerOpen = ref(false)

function toggleLeftDrawer() {
  leftDrawerOpen.value = !leftDrawerOpen.value
}
</script>

<style>
/* GLOBAL */
body {
  background: #100c18;
  color: #f5efff;
  font-family: 'Segoe UI', sans-serif;
}

.library-layout {
  background: #100c18;
}

/* HEADER */
.library-header {
  background: #171020;
  border-bottom: 1px solid #39234e;
  color: white;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.35);
}

.toolbar {
  min-height: 75px;
  padding: 0 25px;
}

.menu-btn {
  color: #c69aff;
  margin-right: 15px;
}

.brand {
  display: flex;
  align-items: center;
  gap: 12px;
  color: #c69aff;
}

.brand-title {
  font-size: 23px;
  font-weight: 800;
  letter-spacing: 1px;
  color: white;
}

.brand-subtitle {
  display: block;
  font-size: 9px;
  letter-spacing: 3px;
  color: #ad82d9;
  margin-top: -3px;
}

.header-right {
  display: flex;
  align-items: center;
  gap: 10px;
  color: #bba7ce;
  font-size: 13px;
}

/* DRAWER */
.library-drawer {
  background: #171020 !important;
  color: white;
  border-right: 1px solid #39234e !important;
}

.drawer-content {
  height: 100%;
  display: flex;
  flex-direction: column;
  padding: 25px 16px;
}

.drawer-logo {
  display: flex;
  align-items: center;
  gap: 13px;
  padding: 10px 8px 25px;
}

.logo-icon {
  width: 52px;
  height: 52px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: linear-gradient(135deg, #7828b9, #42146b);
  border-radius: 15px;
  color: white;
  box-shadow: 0 4px 18px rgba(147, 61, 209, 0.3);
}

.logo-title {
  font-size: 16px;
  font-weight: 800;
  letter-spacing: 2px;
  color: #e8d4ff;
}

.logo-caption {
  font-size: 11px;
  color: #9985aa;
  margin-top: 4px;
}

.drawer-separator {
  background: #392746;
  margin-bottom: 25px;
}

.menu-heading {
  color: #9175a8;
  font-size: 10px;
  font-weight: bold;
  letter-spacing: 2px;
  padding: 0 12px 15px;
}

.navigation-list {
  display: flex;
  flex-direction: column;
  gap: 7px;
}

/* FOOTER */
.drawer-footer {
  margin-top: auto;
  padding: 18px 10px 5px;
  border-top: 1px solid #392746;
  display: flex;
  align-items: center;
  gap: 9px;
  font-size: 11px;
  color: #a895b7;
}

/* PAGE */
.page-container {
  background:
    radial-gradient(
      circle at top right,
      rgba(113, 45, 153, 0.13),
      transparent 35%
    ),
    #100c18;
  min-height: 100vh;
}

/* RESPONSIVE */
@media (max-width: 600px) {
  .toolbar {
    padding: 0 12px;
  }

  .header-right {
    display: none;
  }

  .brand-title {
    font-size: 20px;
  }
}
</style>

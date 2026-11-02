
<template>
  <q-page class="about-page q-pa-lg">

    <div class="page-heading">
      <div class="heading-icon">
        <q-icon name="info" size="38px" />
      </div>

      <div>
        <div class="page-title">O našoj knjižnici</div>
        <div class="page-subtitle">
          Upoznajte Gradsku knjižnicu Rijeka.
        </div>
      </div>
    </div>

    <q-card class="about-card">

      <div class="hero-image">
        <q-img
          src="https://www.rijeka.hr/wp-content/uploads/2023/12/Nova-knji%C5%BEnica-4-901x600.jpg"
          class="about-image"
          :ratio="16 / 7"
          fit="cover"
        >
          <template v-slot:error>
            <div class="image-error">
              <q-icon name="menu_book" size="65px" />
              <div>Gradska knjižnica Rijeka</div>
            </div>
          </template>

          <div class="image-overlay">
            <div class="image-label">DOBRODOŠLI U NAŠU KNJIŽNICU</div>
            <div class="image-title">O nama</div>
            <div class="image-caption">
              Mjesto znanja, kulture i inspiracije.
            </div>
          </div>
        </q-img>
      </div>

      <q-card-section class="about-content">

        <div class="section-title">
          <q-icon name="auto_stories" color="purple-4" size="28px" />
          Tko smo mi?
        </div>

        <p class="about-text">
          {{ o_nama }}
        </p>

        <q-separator class="about-separator" />

        <div class="section-title q-mb-md">
          <q-icon name="stars" color="purple-4" size="27px" />
          Naša uloga
        </div>

        <div class="features-grid">

          <div class="feature-item">
            <q-icon name="menu_book" size="32px" />
            <div class="feature-title">Znanje</div>
            <div class="feature-description">
              Bogat izbor knjiga i literature.
            </div>
          </div>

          <div class="feature-item">
            <q-icon name="school" size="32px" />
            <div class="feature-title">Obrazovanje</div>
            <div class="feature-description">
              Potpora učenju i istraživanju.
            </div>
          </div>

          <div class="feature-item">
            <q-icon name="groups" size="32px" />
            <div class="feature-title">Zajednica</div>
            <div class="feature-description">
              Mjesto susreta i druženja.
            </div>
          </div>

        </div>

      </q-card-section>
    </q-card>

    <div class="bottom-text">
      <q-icon name="favorite" color="purple-4" />
      Knjige povezuju ljude i stvaraju nove svjetove.
    </div>

  </q-page>
</template>

<script>
export default {
  setup () {
    const o_nama = 'Gradska knjižnica Rijeka središnja je narodna knjižnica grada Rijeke i matična knjižnica za narodne i školske knjižnice Primorsko-goranske županije. Ona je informacijsko, obrazovno, kulturno, komunikacijsko i socijalno središte Rijeke i okolice usmjereno prema novom stvaralaštvu, održivom razvoju i kvaliteti razvoja zajednice i čitateljske kulture.'

    return {
      o_nama
    }
  }
}
</script>

<style scoped>
.about-page {
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

.about-card {
  background: #191221;
  border: 1px solid #49305d;
  border-radius: 18px;
  overflow: hidden;
  box-shadow: 0 8px 30px rgba(0, 0, 0, 0.25);
}

.about-image {
  width: 100%;
}

.image-overlay {
  position: absolute;
  inset: 0;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
  background: linear-gradient(
    0deg,
    rgba(18, 10, 27, 0.95),
    rgba(50, 20, 75, 0.25)
  );
}

.image-label {
  color: #d6aaff;
  font-size: 11px;
  letter-spacing: 3px;
  font-weight: bold;
}

.image-title {
  font-size: 48px;
  font-weight: bold;
  color: white;
  margin-top: 10px;
}

.image-caption {
  color: #eadcf7;
  font-size: 14px;
  margin-top: 5px;
}

.image-error {
  height: 100%;
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 12px;
  color: #d5a8ff;
  background: #291638;
  font-size: 18px;
}

.about-content {
  padding: 30px;
}

.section-title {
  display: flex;
  align-items: center;
  gap: 12px;
  font-size: 22px;
  font-weight: bold;
  color: #eadbfa;
}

.about-text {
  color: #b8a7c7;
  font-size: 15px;
  line-height: 1.9;
  text-align: justify;
  margin-top: 20px;
}

.about-separator {
  background: #49305d;
  margin: 25px 0;
}

.features-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 15px;
}

.feature-item {
  background: #251831;
  border: 1px solid #49305d;
  border-radius: 14px;
  padding: 22px 15px;
  text-align: center;
  color: #c99bf0;
  transition: 0.3s;
}

.feature-item:hover {
  background: #352044;
  transform: translateY(-4px);
}

.feature-title {
  color: #eee0ff;
  font-size: 15px;
  font-weight: bold;
  margin-top: 12px;
}

.feature-description {
  color: #a895b7;
  font-size: 12px;
  margin-top: 7px;
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

  .image-title {
    font-size: 30px;
  }

  .image-label {
    font-size: 8px;
  }

  .image-caption {
    font-size: 11px;
  }

  .features-grid {
    grid-template-columns: 1fr;
  }

  .about-content {
    padding: 20px;
  }
}
</style>

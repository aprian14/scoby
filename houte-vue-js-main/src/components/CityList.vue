<template>
  <div id="CityList">
    <!-- Recommendation Hotel Based City List -->
    <div class="rec-list-city">
      <div class="container">
        <div class="row">
          <div class="col-lg-3" v-for="kota in listkota.kota" :key="kota.id" >
            <div
              class="img-city"
              :style="{ 'background-image': 'url(http://localhost:8000/storage/' + kota.cover + ')' }"
            >
              <div class="text-banner">
                <h5>
                  {{ kota.nama_kota }}
                </h5>
                <p>100+ Akomodasi</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- Recommendation Hotel Based City List End-->
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "CityList",

  // siapkan variabel penerima data dari web service atau data apapun yg ingin diwadahi
  data() {
    return {
      listkota: [],
      response: {},
    };
  },

  // siapkan function request web service dsb
  methods: {
    // fungsi untuk menjalankan hasil request web service
    setData(dataAPI) {
      // mengisikan nilai pada variabel listkota
      this.listkota = dataAPI;
    },

    // fungsi untuk request web service
    async getDataKota() {
      try {
        // request data ke endpoint web service
        this.response = await axios.get("http://127.0.0.1:8000/api/list-kota");

        // panggil function setData dan isikan hasil request web service ke dalam parameter dataAPI yg ada di function setData
        this.setData(this.response.data);

        console.log(this.response.data);
      } catch (error) {
        console.log(error);
      }
    },
  },

  // function yg ingin dijalankan saat halaman dirender
  mounted() {
    this.getDataKota();
  },
};
</script>

<style>
.rec-list-city .col-lg-3 .img-city {
  width: 100%;
  height: 382px;
  background-size: cover;
  border-radius: 10px;
}

.rec-list-city .col-lg-3 .text-banner h5 {
  text-align: left;
  margin-bottom: 10px;
}
</style>
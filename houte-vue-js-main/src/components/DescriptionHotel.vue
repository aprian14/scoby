<template>
  <div id="desc-hotel">
    <div class="container" id="detail-title">
      <div class="row justify-content-between align-items-center">
        <div class="col-lg-6">
          <img :src="'http://localhost:8000/storage/' + hotel.gambar" alt="amaris-hotel" />
        </div>
        <div class="col-lg-5">
          <h1 class="mb-4">{{ hotel.nama_hotel }}</h1>
          <p class="mb-4">{{ hotel.alamat }} - {{ hotel.nama_kota }}</p>
          <div class="ratings d-flex mt-4">
            <img src="../assets/star-icon.png" alt="star" />
            <img src="../assets/star-icon.png" alt="star" />
            <img src="../assets/star-icon.png" alt="star" />
            <img src="../assets/star-icon.png" alt="star" />
            <img src="../assets/star-icon.png" alt="star" />
            <p class="star-text">{{ hotel.rating }} Rate</p>
          </div>
          <router-link :to="'/PaymentPage/' + hotel.id" class="btn btn-primary my-4"
            >Pesan Sekarang!</router-link
          >
        </div>
      </div>
    </div>

    <div class="container">
      <div class="row my-5 align-items-center justify-content-between">
        <div class="col-lg-6">
          <h1 class="fw-bold">Deskripsi</h1>
          <div class="my-4">
            <div v-html="hotel.deskripsi"></div>
          </div>
        </div>
        <div class="col-lg-5">
          <h6 class="fw-bold">Fasilitas</h6>
          <div class="d-flex align-items-center gap-4 my-4">
            <img src="../assets/wifi-icon.png" />
            <p class="my-0">Wifi Gratis</p>
          </div>
          <div class="d-flex align-items-center gap-4 my-4">
            <img src="../assets/credit-card-icon.png" />
            <p class="my-0">Pembayaran Kartu</p>
          </div>
          <div class="d-flex align-items-center gap-4 my-4">
            <img src="../assets/cctv-icon.png" />
            <p class="my-0">Kamera CCTV</p>
          </div>
          <div class="d-flex align-items-center gap-4 my-4">
            <img src="../assets/stove-icon.png" />
            <p class="my-0">Dapur</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "DescriptionHotel",

  // siapkan variabel penerima data dari web service atau data apapun yg ingin diwadahi
  data() {
    return {
      hotel: {},
      response: {},
    };
  },

  // siapkan function request web service dsb
  methods: {
    // fungsi untuk menjalankan hasil request web service
    setData(dataAPI) {
      // mengisikan nilai pada variabel hotel
      this.hotel = dataAPI;
    },

    // fungsi untuk request web service
    async getDetailHotel() {
      try {
        this.response = await axios.get(
          "http://127.0.0.1:8000/api/detail-hotel/" +
            this.$route.params.id
        );

        // panggil function setData dan isikan hasil request web service ke dalam parameter dataAPI yg ada di function setData
        this.setData(this.response.data.hotel);

        console.log(this.response.data);
      } catch (error) {
        console.log(error);
      }
    },
  },

  // function yg ingin dijalankan saat halaman dirender
  mounted() {
    this.getDetailHotel();
  },
};
</script>

<style>
#detail-title .col-lg-6 img {
  width: 100%;
  border-radius: 10px;
}

#detail-title .col-lg-5 .ratings {
  gap: 20px;
}

@media only screen and (max-width: 992px) {
  #detail-title .col-lg-5 {
    text-align: center;
    margin-top: 20px;
  }
}
</style>
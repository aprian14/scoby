<template>
  <div id="HeroBanner">
    <!-- Hero -->
    <section id="hero">
      <div class="container">
        <div class="row">
          <div class="col-lg-12 banner" :style="{ 'background-image': 'url(http://localhost:8000/storage/' + listbanner.gambar_banner + ')' }">
            <div class="text-banner">
              <h1>Nikmati Liburan Yang Di Impikan.</h1>
              <p>
                Liburan di Hotel dengan Fasilitas Nyaman Hanya ada di Houtel!
              </p>
              <button type="button" class="btn btn-primary">
                Booking Sekarang!
              </button>
            </div>
          </div>
        </div>
      </div>
    </section>
    <!-- Hero End -->
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "HeroBanner",
  // siapkan variabel penerima data dari web service atau data apapun yg ingin diwadahi
  data() {
    return {
      // variabel untuk menampung nilai keyword
      keyword: "",
      listbanner: [],
      response: {},
    };
  },

  // siapkan function request web service dsb
  methods: {
    // fungsi untuk menjalankan hasil request web service
    setData(dataAPI) {
      // mengisikan nilai pada variabel listbanner
      this.listbanner = dataAPI;
    },

    // fungsi untuk request web service
    async getDataBanner() {
      try {
        // request data ke endpoint web service
        this.response = await axios.get(
          "http://127.0.0.1:8000/api/list-banner?posisi=Atas"
        );

        // panggil function setData dan isikan hasil request web service ke dalam parameter dataAPI yg ada di function setData
        this.setData(this.response.data.banner);

        console.log(this.response.data.banner);
      } catch (error) {
        console.log(error);
      }
    },
  },

  // function yg ingin dijalankan saat halaman dirender
  mounted() {
    console.log("Haloo");
    this.getDataBanner();
  },
};
</script>

<style>
/* Hero */
#hero .col-lg-12,
.rec-list-city .col-lg-3 {
  position: relative;
  color: white;
  justify-content: center;
}

#hero .col-lg-12.banner {
  /* background: url(../assets/banner.png); */
  width: 100%;
  height: 395px;
  background-size: cover;
  border-radius: 10px;
}

#hero .col-lg-12.banner .text-banner {
  width: 375px;
  margin-top: 90px;
  margin-left: 53px;
}

#hero form input {
  width: 600px;
}
/* Hero End */
</style>
<template>
  <div class="row g-0">
    <div class="container">
      <CarouselVue />
    </div>
    <!-- STRUK -->
    <div class="col-md-4 my-4">
      <div class="card mx-5 my-3 px-3" id="struk" style="display:block; position: sticky; top: 80px;">
          <ul class="list-group list-group-flush justify-content-start" style="width: 100%">
            <li class="list-group-item" style="background-color: #fbf2bf; ">
              <h5 class="my-3"> Price Details</h5>
              <h6 style="font-weight:normal">Sub Total &emsp;&nbsp; Rp. 140.000</h6>
              <h6 style="font-weight:normal">PPN 10% &emsp;&nbsp; Rp. 14.000</h6>
            </li>
            <li class="list-group-item" style="background-color: #fbf2bf">
              <h6 style="font-weight:bold"> Total &emsp;&emsp;&emsp; Rp. 154.000</h6>
              <div class="d-grid">
                <button class="btn btn-success my-3" type="button">Checkout</button>
              </div>
              <p class="my-2" style="text-align:center; color: red;">Silahkan Lakukan Pembayaran Dengan <br>Menyebutkan Username Anda</p>
              <br><br>
            </li>
          </ul>
        </div>
    </div>

    <!-- CARTS DATA -->
    <div class="col-md-8 my-4">
      <div class="container-fluid">
        <section class="carts">
          <div v-for="produk in carts" :key="produk.id" class="produk">
            <div class="card mt-3" style="width: 60%">
              <div class="row g-1">
                <div class="col-md-4 ml-2">
                  <img
                    src="../assets/Rectangle4.svg"
                    class="img-fluid"
                    style="width: 100%; height: 100%"
                  />
                </div>
                <div class="col-md-8" :key="produk.id">
                  <div class="card-body">
                    <h5 class="card-title">{{ produk.nama_makanan }}</h5>
                    <p class="card-text">
                      {{ produk.harga_makanan }}
                      <br />

                      <span
                        class="badge"
                        type="button"
                        @click="updateCart(produk, 'tambah')"
                        style="backgorund-color: #59cfd7"
                        >+</span
                      >
                      <span class="badge" style="background-color:#fbf2bf ">{{
                        produk.kuantitas
                      }}</span>
                      <span
                        class="badge"
                        type="button"
                        @click="updateCart(produk, 'kurang')"
                        style="backgorund-color: #59cfd7"
                        >-</span
                      >
                    </p>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </section>
        <br><br>
      </div>
    </div>
  </div>
</template>

<script>
import CarouselVue from "../components/CarouselVue.vue";

export default {
  name: "LihatKeranjang",
  data() {
    return {
      carts: [
        {
          id: 1,
          nama_makanan: "Udang Mentega",
          harga_makanan: "35.000",
          kuantitas: 1,
        },

        {
          id: 2,
          nama_makanan: "Udang Mentega Pedas",
          harga_makanan: "35.000",
          kuantitas: 1,
        },

        {
          id: 3,
          nama_makanan: "Udang Mentega Manis",
          harga_makanan: "35.000",
          kuantitas: 1,
        },
        {
          id: 4,
          nama_makanan: "Udang Mentega Manis",
          harga_makanan: "35.000",
          kuantitas: 1,
        },
        {
          id: 5,
          nama_makanan: "Udang Mentega Manis",
          harga_makanan: "35.000",
          kuantitas: 1,
        },
        {
          id: 6,
          nama_makanan: "Udang Mentega Manis",
          harga_makanan: "35.000",
          kuantitas: 1,
        },
      ],
    };
  },
  computed: {
    jumlah_pesanan() {
      return this.carts.reduce((total, produk) => total + produk.kuantitas, 0);
    },
  },
  methods: {
    updateCart(produk, updateType) {
      for (let i = 0; i < this.carts.length; i++) {
        if (this.carts[i].id === produk.id) {
          if (updateType === "kurang") {
            if (this.carts[i].kuantitas !== 0) {
              this.carts[i].kuantitas--;
            }
          } else {
            this.carts[i].kuantitas++;
          }

          break;
        }
      }
      console.log(this.carts);
    },
  },

  components: {
    CarouselVue: CarouselVue,
  },
};
</script>

<style scoped>
.card {
  border: 0px;
  border-radius: 25px;
  background: #fafafa;
}
.card-title,
.card-text {
  color: #3a556a;
}

span {
  margin: 8px 5px 0px 5px;
  font-weight: bold;
  font-size: 1rem;
  color: #3a556a;
  background-color: #59cfd7;
}
.d-grid {
  margin-top: 20px;
}

h5 {
  margin-bottom: 0px;
}
ul {
  width: 60%;
  background-color: #fbf2bf;
}
#img-1 {
  position: relative;
}

#img-2 {
  position: relative;
  z-index: 1;
  /* left: -25px; */
  right: 28px;
}

#struk{
  width: 60%;
  border-radius: 10px;
  background-color: #fbf2bf;
}
</style>


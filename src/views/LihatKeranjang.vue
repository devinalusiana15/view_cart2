<template>
  <div class="row g-0">
    <div class="container">
      <CarouselVue />
    </div>
    <!-- STRUK -->
    
    <div class="col-md-4 my-4" >
      <div class="card mx-5 my-3 px-3" id="struk" style="display:block; position: sticky; top: 80px;">
          <ul class="list-group list-group-flush justify-content-start" style="width: 100%">
            <li class="list-group-item" style="background-color: #fbf2bf; ">
              <h5 class="my-3"> Price Details</h5>
              <h6 style="font-weight:normal">Sub Total &emsp;&nbsp; Rp. {{carts.total_harga}} </h6>
              <h6 style="font-weight:normal">PPN 10% &emsp;&nbsp; Rp. {{carts.total_harga*0.1}}</h6>
            </li>
            <li class="list-group-item" style="background-color: #fbf2bf">
              <h6 style="font-weight:bold"> Total &emsp;&emsp;&emsp; Rp. {{carts.total_harga+carts.total_harga*0.1}}</h6>
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
          <div v-for="item in carts.produk" :key="item.nama_produk" class="produk">
            <div class="mb-5 row justify-content-center ">
              <div class="col">
                <img
                      src="../assets/Rectangle4.svg"
                      class="img-fluid"
                      style="width: 100%; height: 100%"
                    />
              </div>
              <div class="col">
                <h5 class="card-title">{{ item.nama_produk }}</h5>
                              <p class="col-md-12 card-text">
                          {{ item.harga_produk }}
                          <br />

                          <span
                            class="badge"
                            type="button"
                            @click="updateCart(item, 'kurang')"
                            style="backgorund-color: #59cfd7"
                            >-</span
                          >
                          <span class="badge" style="background-color:#fbf2bf ">{{ item.kuantitas }}</span>
                          <span
                            class="badge"
                            type="button"
                            @click="updateCart(item, 'tambah')"
                            style="backgorund-color: #59cfd7"
                            >+</span
                          >
                          </p>
              </div>
                  <div class="col">
                  <br />
                      <span class="badge" style="background-color:#fbf2bf; font-weight: 400; width: 199px; height: 30px;">Rp. {{item.harga_produk*item.kuantitas }}</span>
                  </div>
            </div>
              <!-- <div class="card mt-3" style="width: 60%">
                <div class="row g-1">
                  <div class="col-md-4 ml-2">
                    <img
                      src="../assets/Rectangle4.svg"
                      class="img-fluid"
                      style="width: 100%; height: 100%"
                    />
                  </div>
                  <div class="col-md-8">
                    <div class="card-body">
                      
                        <div class="row justify-content-cente align-items-center">

                          <div class="col">
                            <h5 class="card-title">{{ item.nama_produk }}</h5>
                              <p class="col-md-12 card-text">
                          {{ item.harga_produk }}
                          <br />

                          <span
                            class="badge"
                            type="button"
                            @click="updateCart(item, 'tambah')"
                            style="backgorund-color: #59cfd7"
                            >+</span
                          >
                          <span class="badge" style="background-color:#fbf2bf ">{{ item.kuantitas }}</span>
                          <span
                            class="badge"
                            type="button"
                            @click="updateCart(item, 'kurang')"
                            style="backgorund-color: #59cfd7"
                            >-</span
                          >
                          </p>
                          </div>
                          <div class="col">
                            <span class="badge" style="background-color:#fbf2bf; font-weight: 400;">Rp. {{item.harga_total }}</span>
                          </div>
                        </div>
                      </div>
                    </div>
                  </div>
                </div> -->
            </div>
        </section>
        <br><br>
      </div>
    </div>
  </div>
</template>

<script>
import CarouselVue from "../components/CarouselVue.vue";
import axios from "axios";

export default {
  name: "LihatKeranjang",
  data() {
    return {
      carts: [],
    };
  },
  computed: {
    jumlah_pesanan() {
      return this.carts.reduce((total, produk) => total + produk.kuantitas, 0);
    },
  },
  methods: {
      updateCart(item, updateType) {      
              if (updateType === 'kurang') {
                if (item.kuantitas !== 0) {
                  item.kuantitas--;
                }
              } else {
               item.kuantitas++;
              }
            },

      setproduk(data){
         this.carts = data.cart
      },

      chekOut(){
        axios
        .patch("http://localhost:3000/api/cart/635f4f806c23111df8ddfe3e",{
          productName:this.carts.nama_produk,
          kuantitas:this.carts.kuantitas
        })
      }  
  },

  components: {
    CarouselVue: CarouselVue,
  },

  mounted(){
    axios
    .get("http://localhost:3000/api/cart/635f4f806c23111df8ddfe3e")
     .then((response) => this.setproduk(response.data))
    // .then(response => console.log(response.data.cart.produk[0].nama_produk))
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


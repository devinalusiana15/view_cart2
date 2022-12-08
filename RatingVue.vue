<template>
  <div
    class="modal fade"
    id="exampleModal"
    tabindex="-1"
    aria-labelledby="exampleModalLabel"
    aria-hidden="true"
  >
    <div class="modal-dialog modal-dialog-centered modal-sm">
      <div class="modal-content">
        <div class="modal-body">
          <form v-on:submit.prevent>
            <div class="col-auto">
              <h2 class="text-center my-2" id="title">Rating</h2>
              <!-- STAR -->
              <div class="container">
                <div
                  class="
                    starrating
                    risingstar
                    d-flex
                    justify-content-center
                    flex-row-reverse
                  "
                >
                  <input
                    type="radio"
                    id="star5"
                    name="rating"
                    value="5"
                    v-model="rating.rating"
                  /><label for="star5" title="5 star"
                    ><i class="fa-regular fa-star"></i
                  ></label>
                  <input
                    type="radio"
                    id="star4"
                    name="rating"
                    value="4"
                    v-model="rating.rating"
                  /><label for="star4" title="4 star"
                    ><i class="fa-regular fa-star"></i
                  ></label>
                  <input
                    type="radio"
                    id="star3"
                    name="rating"
                    value="3"
                    v-model="rating.rating"
                  /><label for="star3" title="3 star"
                    ><i class="fa-regular fa-star"></i
                  ></label>
                  <input
                    type="radio"
                    id="star2"
                    name="rating"
                    value="2"
                    v-model="rating.rating"
                  /><label for="star2" title="2 star"
                    ><i class="fa-regular fa-star"></i
                  ></label>
                  <input
                    type="radio"
                    id="star1"
                    name="rating"
                    value="1"
                    v-model="rating.rating"
                  /><label for="star1" title="1 star"
                    ><i class="fa-regular fa-star"></i
                  ></label>
                </div>
              </div>
              <textarea
                class="form-control mx-auto"
                placeholder="Beri penilaian terhadap restoran ini"
                id="floatingTextarea2"
                v-model="rating.review"
              ></textarea>
              <br /><br />
            </div>
          </form>
        </div>
        <div class="d-grid gap-1 col-8 mx-auto">
          <button
            class="btn btn-success"
            id="content"
            type="button"
            @click="rate"
            data-bs-dismiss="modal"
          >
            Send
          </button>
          <p
            class="text-center"
            id="content"
            type="button"
            data-bs-dismiss="modal"
          >
            Lewati
          </p>
        </div>
        <br />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Swal from "sweetalert2";
export default {
  name: "RatingVue",
  data() {
    return {
      rating: {},
    };
  },
  methods: {
    rate() {
      axios
        .post("http://localhost:3000/api/review", this.rating)
        .then(() => {
          console.log("Berhasil");
          Swal.fire("Terima kasih!", "Penilaian Anda telah kami terima", "success");
        })
        .catch((err) => console.log(err));
    },
  },
};
</script>

<style scoped>
@import url(https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.2.0/css/all.min.css);
@import url(https://fonts.googleapis.com/css2?family=Poppins:wght@500;600;700&family=Roboto:wght@100;300;400;500;700;900&family=Volkhov&display=swap);
@import url(https://fonts.googleapis.com/css2?family=Lexend+Deca&family=Poppins:wght@500;600;700&family=Roboto:wght@100;300;400;500;700;900&display=swap);

.modal-content {
  background-color: #f5f5f5;
}

.btn-success {
  background-color: #6a983c !important;
}

#title {
  font-family: "Volkhov", serif;
}

/* Remove radio buttons */
.starrating > input {
  display: none;
}

#content {
  font-family: "Lexend Deca", sans-serif;
}

.starrating > label {
  position: relative;
  width: 1em;
  font-size: 25px;
  margin: 10px;
  font-weight: 300;
  color: #ffd600;
  cursor: pointer;
}

/* Star */
.starrating > label:before {
  font-family: "FontAwesome";
  content: "\f005";
  position: absolute;
  opacity: 0;
}
.starrating > label:hover:before,
.starrating > label:hover ~ label:before {
  opacity: 1 !important;
}

.starrating > input:checked ~ label:before {
  opacity: 1;
}

.starrating:hover > input:checked ~ label:before {
  opacity: 0.4;
}

textarea {
  height: 100px;
  width: 250px;
  border-radius: 15px;
}
</style>
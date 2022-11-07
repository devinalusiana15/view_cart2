<template>
  <!-- NAVBAR -->
  <NavbarVue />
  <!-- Fitur lihat keranjang -->
  <LihatKeranjangVue />
  <!-- Footer   -->
  <FooterVue />
</template>

<script>
import NavbarVue from "./components/NavbarVue";
import FooterVue from "./components/FooterVue.vue";
import LihatKeranjangVue from "./views/LihatKeranjang.vue";

export default {
  data() {
    return {
    };
  },

  components: {
    NavbarVue: NavbarVue,
    FooterVue: FooterVue,
    LihatKeranjangVue: LihatKeranjangVue,
  },

};
</script>





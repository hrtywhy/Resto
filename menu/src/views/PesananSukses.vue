<template>
  <div class="pesanan-sukses">
    <Navbar />
    <div class="container">
        <div class="row justify-content-center mt-5">
            <div class="col text-center">
                <img src="../assets/image/wait.png" width="300" />
              <h2><strong>Sukses!</strong></h2>
              <h2>Pesanan Anda segera diproses <br> Selamat Menunggu</h2>
            </div>
        </div>
    </div>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
export default {
  name: "PesananSukses",
  components: {
    Navbar,
  },
};
</script>

<style>
</style>
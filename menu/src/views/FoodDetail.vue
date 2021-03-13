<template>
  <div class="food-detail">
    <navbar />
    <div class="container">
      <!-- breadcrumb -->
      <div class="row mt-4">
        <div class="col">
          <nav aria-label="breadcrumb">
            <ol class="breadcrumb">
              <li class="breadcrumb-item">
                <router-link to="/" class="text-dark">Home</router-link>
              </li>
              <li class="breadcrumb-item">
                <router-link to="/foods" class="text-dark">Food</router-link>
              </li>
              <li class="breadcrumb-item active" aria-current="page">
                Food Order
              </li>
            </ol>
          </nav>
        </div>
      </div>

      <div class="row mt-3">
        <div class="col md-6">
          <img
            :src="'../assets/images/' + product.gambar"
            class="img-fluid shadow"
          />
        </div>
        <div class="col md-6">
          <h2>
            <strong>{{ product.nama }}</strong>
          </h2>
          <hr />
          <h4>
            Harga : <strong>Rp. {{ product.harga }}</strong>
          </h4>
          <form class="mt-4" v-on:submit.prevent>
            <div class="form-group">
              <label for="jumlah-pemesanan">Jumlah Pesan</label>
              <input
                type="number"
                class="form-control"
                v-model="pesan.jumlah_pemesanan"
              />
            </div>
            <div class="form-group">
              <label for="ketereangan">Keterangan</label>
              <textarea
                v-model="pesan.keterangan"
                class="form-control"
              ></textarea>
            </div>
            <button type="submit" class="btn btn-success" @click="pemesanan">
              <b-icon-cart></b-icon-cart>Pesan
            </button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import navbar from "@/components/navbar.vue";
import axios from "axios";

export default {
  name: "FoodDetail",
  components: {
    navbar,
  },
  data() {
    return {
      product: {},
      pesan: {},
    };
  },
  methods: {
    setProduct(data) {
      this.product = data;
    },
    pemesanan() {
      if (this.pesan.jumlah_pemesanan) {
        this.pesan.products = this.products;
        axios
          .post("http://localhost:3000/keranjangs", this.pesan)
          .then(() => {
            this.$router.push({path: "/keranjang"})
            this.$toast.success("Sukses Masuk Keranjang", {
              type: "success",
              position: "top-right",
              duration: 3000,
              dismissible: true,
            });
          })
          .catch((error) => console.log(error));
      } else {
        this.$toast.error("Jumlah pesanan harus diisi", {
          type: "error",
          position: "top-right",
          duration: 3000,
          dismissible: true,
        });
      }
    },
  },
  mounted() {
    axios
      .get("http://localhost:3000/products/" + this.$route.params.id)
      .then((response) => this.setProduct(response.data))
      .catch((error) => console.log(error));
  },
};
</script>

<style>
</style>
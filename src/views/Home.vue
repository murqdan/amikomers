<template>
  <div class="home">
    <section class="hero is-medium mb-6">
      <div class="images">
        <div class="image">
          <img src="../assets/banner.png" />
        </div>
      </div>
    </section>

    <div class="columns is-multiline">
      <div class="column is-12">
        <h2 class="is-size-2 has-text-centered">Kategori</h2>
      </div>
      <div class="column is-3">
        <router-link
          to="/laptop"
          class="button is-fullwidth"
          style="
            height: 65px;
            font-weight: 600;
            background-color: #4a2497;
            color: white;
          "
          >Laptop</router-link
        >
      </div>
      <div class="column is-3">
        <router-link
          to="/mouse"
          class="button is-fullwidth"
          style="
            height: 65px;
            font-weight: 600;
            background-color: #4a2497;
            color: white;
          "
          >Mouse</router-link
        >
      </div>
      <div class="column is-3">
        <router-link
          to="/monitor"
          class="button is-fullwidth"
          style="
            height: 65px;
            font-weight: 600;
            background-color: #4a2497;
            color: white;
          "
          >Monitor</router-link
        >
      </div>
      <div class="column is-3">
        <router-link
          to="/keyboard"
          class="button is-fullwidth"
          style="
            height: 65px;
            font-weight: 600;
            background-color: #4a2497;
            color: white;
          "
          >Keyboard</router-link
        >
      </div>
    </div>

    <div class="columns is-multiline">
      <div class="column is-12">
        <h2 class="is-size-2 has-text-centered">Produk Terbaru</h2>
      </div>

      <ProductBox
        v-for="product in latestProducts"
        v-bind:key="product.id"
        v-bind:product="product"
      />
    </div>
  </div>
</template>

<script>
import axios from 'axios';

import ProductBox from '@/components/ProductBox';

export default {
  name: 'Home',
  data() {
    return {
      latestProducts: [],
    };
  },
  components: {
    ProductBox,
  },
  mounted() {
    this.getLatestProducts();

    document.title = 'Amikomers. | Rusak? Beli Lagi!';
  },
  methods: {
    async getLatestProducts() {
      this.$store.commit('setIsLoading', true);

      await axios
        .get('/api/v1/latest-products/')
        .then((response) => {
          this.latestProducts = response.data;
        })
        .catch((error) => {
          console.log(error);
        });

      this.$store.commit('setIsLoading', false);
    },
  },
};
</script>

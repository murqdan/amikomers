<template>
  <div id="wrapper">
    <nav class="navbar" style="background-color: #4a2497">
      <div class="navbar-brand">
        <router-link to="/" class="navbar-item">
          <img src="./assets/amikomers-logo.png" alt="" />
          <strong
            style="
              font-size: 23px;
              color: white;
              padding-left: 6px;
              padding-top: 10px;
            "
            >Amikomers.</strong
          ></router-link
        >

        <a
          class="navbar-burger"
          aria-label="menu"
          aria-expanded="false"
          data-target="navbar-menu"
          style="
            color: white;
            margin-top: 13px;
            background-color: unset !important;
          "
        >
          <span aria-hidden="true"></span>
          <span aria-hidden="true"></span>
          <span aria-hidden="true"></span>
        </a>
      </div>

      <div class="navbar-menu" id="navbar-menu">
        <div class="navbar-start">
          <div class="navbar-item">
            <form method="get" action="/search">
              <div class="field has-addons">
                <div class="control">
                  <input
                    type="text"
                    class="input"
                    placeholder="cari sesuatu.."
                    name="query"
                  />
                </div>

                <div class="control">
                  <button class="button" style="background-color: #ff9b39">
                    <span class="icon">
                      <i
                        class="fas fa-search"
                        style="filter: brightness(0) invert(1)"
                      ></i>
                    </span>
                  </button>
                </div>
              </div>
            </form>
          </div>
        </div>

        <div class="navbar-end">
          <div class="navbar-item">
            <div class="buttons">
              <router-link to="/cart" class="button is-info">
                <span class="icon"><i class="fas fa-shopping-cart"></i></span>
                <span>({{ cartTotalLength }})</span>
              </router-link>

              <template v-if="$store.state.isAuthenticated">
                <router-link
                  to="/my-account"
                  class="button is-light"
                  style="background-color: #ff9b39"
                  ><strong style="color: white">Akun saya</strong></router-link
                >
              </template>

              <template v-else>
                <router-link to="/log-in" class="button is-outlined"
                  ><strong style="color: gray">Masuk</strong></router-link
                >
                <router-link
                  to="/sign-up"
                  class="button is-outlined"
                  style="background-color: #ff9b39"
                  ><strong style="color: white">Daftar</strong></router-link
                >
              </template>
            </div>
          </div>
        </div>
      </div>
    </nav>

    <div
      class="is-loading-bar has-text-centered"
      v-bind:class="{ 'is-loading': $store.state.isLoading }"
    >
      <div class="lds-dual-ring"></div>
    </div>

    <section class="section">
      <router-view />
    </section>

    <footer
      class="text-center text-white border-primary border-top border-5"
      style="background-color: #4a2497"
    >
      <!-- Grid container -->
      <div class="container">
        <!-- Section: Links -->
        <section class="mt-5">
          <!-- Grid row-->
          <div class="row text-center d-flex justify-content-center pt-5">
            <!-- Grid column -->
            <div class="col-md-2">
              <h6 class="text-uppercase">
                <strong
                  ><a href="/about" class="text-white">Tentang kami</a></strong
                >
              </h6>
            </div>
            <!-- Grid column -->

            <!-- Grid column -->
            <div class="col-md-2">
              <h6 class="text-uppercase">
                <strong><a href="/" class="text-white">Produk</a></strong>
              </h6>
            </div>
            <!-- Grid column -->

            <!-- Grid column -->
            <div class="col-md-2">
              <h6 class="text-uppercase">
                <strong><a href="/" class="text-white">Penghargaan</a></strong>
              </h6>
            </div>
            <!-- Grid column -->

            <!-- Grid column -->
            <div class="col-md-2">
              <h6 class="text-uppercase">
                <strong><a href="/" class="text-white">Bantuan</a></strong>
              </h6>
            </div>
            <!-- Grid column -->

            <!-- Grid column -->
            <div class="col-md-2">
              <h6 class="text-uppercase">
                <strong><a href="/" class="text-white">Kontak</a></strong>
              </h6>
            </div>
            <!-- Grid column -->
          </div>
          <!-- Grid row-->
        </section>
        <!-- Section: Links -->

        <hr class="mb-0 mt-5" />

        <img src="./assets/amikomers-full-logo.png" alt="amikomers-full-logo" />

        <!-- Section: Text -->
        <section class="mb-5">
          <div class="row d-flex justify-content-center">
            <div class="col-lg-8">
              <p>
                Amikomers adalah platform toko komputer online berbasis web.
                Dengan adanya toko online ini, diharapkan dapat memudahkan
                mahasiswa Amikom untuk membeli keperluan komputer dalam
                melaksanakan kuliah.
              </p>
            </div>
          </div>
        </section>
        <!-- Section: Text -->

        <!-- Section: Social -->
        <section class="text-center mb-5">
          <a href="" class="text-white me-4">
            <i class="fab fa-facebook-f"></i>
          </a>
          <a href="" class="text-white me-4">
            <i class="fab fa-twitter"></i>
          </a>
          <a href="" class="text-white me-4">
            <i class="fab fa-google"></i>
          </a>
          <a href="" class="text-white me-4">
            <i class="fab fa-instagram"></i>
          </a>
          <a href="" class="text-white me-4">
            <i class="fab fa-linkedin"></i>
          </a>
          <a href="" class="text-white me-4">
            <i class="fab fa-github"></i>
          </a>
        </section>
        <!-- Section: Social -->
      </div>
      <!-- Grid container -->

      <!-- Copyright -->
      <div class="text-center p-3" style="background-color: rgba(0, 0, 0, 0.2)">
        <div class="mr-4">
          © 2022 Created by
          <a
            class="text-white"
            href="https://github.com/murqdan"
            target="_blank"
            >Murqdan</a
          >
          - All rights reserved
        </div>
      </div>
      <!-- Copyright -->
    </footer>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      cart: {
        items: [],
      },
    };
  },
  beforeCreate() {
    this.$store.commit('initializeStore');

    const token = this.$store.state.token;

    if (token) {
      axios.defaults.headers.common['Authorization'] = 'Token ' + token;
    } else {
      axios.defaults.headers.common['Authorization'] = '';
    }
  },
  mounted() {
    this.cart = this.$store.state.cart;
  },
  computed: {
    cartTotalLength() {
      let totalLength = 0;

      for (let i = 0; i < this.cart.items.length; i++) {
        totalLength += this.cart.items[i].quantity;
      }

      return totalLength;
    },
  },
};

document.addEventListener('DOMContentLoaded', () => {
  // Get all "navbar-burger" elements
  const $navbarBurgers = Array.prototype.slice.call(
    document.querySelectorAll('.navbar-burger'),
    0
  );

  // Add a click event on each of them
  $navbarBurgers.forEach((el) => {
    el.addEventListener('click', () => {
      // Get the target from the "data-target" attribute
      const target = el.dataset.target;
      const $target = document.getElementById(target);

      // Toggle the "is-active" class on both the "navbar-burger" and the "navbar-menu"
      el.classList.toggle('is-active');
      $target.classList.toggle('is-active');
    });
  });
});
</script>

<style lang="scss">
@import '../node_modules/bulma';
body {
  background-color: #f2f2f2;
}

.lds-dual-ring {
  display: inline-block;
  width: 80px;
  height: 80px;
}
.lds-dual-ring:after {
  content: ' ';
  display: block;
  width: 64px;
  height: 64px;
  margin: 8px;
  border-radius: 50%;
  border: 6px solid #ccc;
  border-color: #ccc transparent #ccc transparent;
  animation: lds-dual-ring 1.2s linear infinite;
}
@keyframes lds-dual-ring {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

.is-loading-bar {
  height: 0;
  overflow: hidden;

  -webkit-transition: all 0.3s;
  transition: all 0.3s;

  &.is-loading {
    height: 80px;
  }
}

.border-primary {
  border-color: #fa962e !important;
}

.is-active {
  background-color: #4a2497;
  box-shadow: none;
}
</style>

<template>
  <div id="app" class="container">
    <main>
      <nav class="navbar navbar-expand-lg navbar-light bg-light" id="nav">
        <img alt="Vue logo" src="./assets/logo.png" width="50px">
        <button
          class="navbar-toggler"
          type="button"
          data-toggle="collapse"
          data-target="#navbarText"
          aria-controls="navbarText"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarText">
          <ul class="navbar-nav mr-auto">
            <li class="nav-item active">
              <router-link to="/" class="nav-link">Home</router-link>
            </li>
            <li class="nav-item">
              <router-link to="/products" class="nav-link">Products</router-link>
            </li>
            <li class="nav-item">
              <router-link to="/about" class="nav-link">About</router-link>
            </li>
          </ul>
          <ul class="navbar-nav ml-auto">
            <li class="nav-item">
              <router-link to="/cart" class="nav-link">
                <i class="fa fa-shopping-cart mr-1">
                  <span class="ml-1">{{this.cartProducts.length}}</span>
                </i>
              </router-link>
            </li>
            <li class="nav-item dropdown" v-if="isLogged()">
              <a
                class="nav-link dropdown-toggle"
                href="#"
                id="navbarDropdownMenuLink"
                role="button"
                data-toggle="dropdown"
                aria-haspopup="true"
                aria-expanded="false"
              >{{this.loggedUser.firstName}}</a>
              <div class="dropdown-menu" aria-labelledby="navbarDropdownMenuLink">
                <router-link to="/" class="dropdown-item">Profile</router-link>
                <!-- <a class="dropdown-item" href="#">Another action</a>
                <a class="dropdown-item" href="#">Something else here</a>-->
                <router-link
                  to="/"
                  class="dropdown-item text-danger"
                  @click.native="loc_logout"
                >Logout</router-link>
              </div>
            </li>
            <li class="nav-item" v-if="!isLogged()">
              <router-link to="/login" class="nav-link">Login</router-link>
            </li>
          </ul>
        </div>
      </nav>
      <router-view/>
    </main>

    <footer class="container-fluid footer text-left mt-3">
      <p class="mr-auto">
        <strong>Pankaj</strong>
      </p>
      <div style="float:right">
        <a href="mailto:testing@gmail.com" style="margin-right:10px">
          <i class="fa fa-envelope-open" aria-hidden="true" style="font-size:20px"></i>
        </a>
        <a href="https://github.com/" target="_blank" style="margin-right:10px">
          <i class="fa fa-github" aria-hidden="true" style="font-size:20px"></i>
        </a>
        <a href="https://www.linkedin.com/" target="_blank" style="margin-right:10px">
          <i class="fa fa-linkedin" aria-hidden="true" style="font-size:20px"></i>
        </a>
      </div>
    </footer>
  </div>
</template>

<script>
// eslint-disable-next-line no-unused-vars
import { mapState, mapActions, mapMutations } from 'vuex'
import {
  isLoggedIn,
  getLoggedInUser
} from './components/shared/service/authService'
export default {
  data () {
    return {
      cartValue: 0
    }
  },
  computed: mapState(['cartProducts', 'loggedUser']),
  methods: {
    /* Initially loading the cart products from local storage */

    ...mapMutations(['SET_CART_PRODUCTS', 'ADD_LOGGED_USER']),

    getLocalProducts () {
      const products = JSON.parse(localStorage.getItem('user-cart'))

      if (products) {
        this.SET_CART_PRODUCTS(products)
      }
    },

    isLogged () {
      return isLoggedIn()
    },

    loc_logout () {
      localStorage.removeItem('_auth')
      this.$router.push('/')
      location.reload()
    }
  },
  created () {
    this.getLocalProducts()

    const loggedUser = getLoggedInUser()

    this.ADD_LOGGED_USER(loggedUser)

    console.log(process.env.NODE_ENV)
    console.log(process.env.VUE_APP_BASE_URL)
  }
}
</script>

<style lang="scss">
// @import url('https://fonts.googleapis.com/css2?family=Special+Elite&display=swap');
@import "../node_modules/bootstrap/dist/css/bootstrap.min.css";

@font-face {

 font-family: 'custom';
  src: url('../src/assets/fonts/edo.ttf') format('truetype');
  font-weight: normal;
  font-style: normal;

}

#app {
  font-family: 'custom';
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#nav {
  padding: 15px;
  a {
    font-weight: bold;
    color: #2c3e50;
    &.router-link-exact-active {
      color: #2547b8;
    }
  }
}

html {
  position: relative;
  min-height: 100%;
}
body {
  margin-bottom: 60px; /* Margin bottom by footer height */
}
.footer {
  position: relative;
  bottom: 0;
  width: 100%;
  height: 60px; /* Set the fixed height of the footer here */
  background-color: #f5f5f5;
}

footer {
  background-color: #f2f2f2;
  padding: 25px;
}

.footer p,
.footer div {
  display: inline;
  vertical-align: top;
  font-family: 'Special Elite', cursive;
  font-size: 20px;
  line-height: 28px;
}
.footer p {
  font-weight: bold;
}

* a {
  color: #2547b8;
}

* .fa {
  font-size: 18px;
}

.buttonGreen-outline {
  width: 100%;
  height: 50px;
  color: #2547b8;
  background-color: #47be8d;
  border-color: #b45353;
  border-radius: 5px;
}
.buttonGreen-outline:hover {
  color: #ffffff;
  background-color: #e6ae46;

}

.buttonGreen {
  color: #fff;
  background-color: #2547b8;
}

.buttonGreen:hover {
  background-color: #2547b8;
}
</style>

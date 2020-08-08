<template>
  <div class="home-component">

    <div class="jumbotron jumbotron-fluid">
        <div class="container">
          <img alt="Vue logo" src="../assets/logo.png" width="350px">
          <br>
          <h3 class="display-5 " style="margin-top: 2.5rem;font-size: xxx-large;"><span style="color: rgb(37, 71, 184);">The Store - For your useless needs</span></h3>
          <p class="lead">Shop here if you are an idiot.</p>
        </div>
    </div>
    <router-link to="/products" tag="button" class="buttonGreen-outline">See Our Products</router-link>

  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
export default {
  name: 'home',
  components: {
    HelloWorld
  }
}
</script>
<style>

.jumbotron {
  background-color: rgb(255, 255, 255);
 font-family: 'custom';
  padding: 1rem 0rem;
}
</style>

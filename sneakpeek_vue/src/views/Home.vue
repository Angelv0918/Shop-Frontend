<template>
  <div class="home">
   <section class="hero is-medium is-light mb-6">
    <div class="hero-body has-text-centered">
      <p class="title mb-6">
        Welcome to Sneakpeek
      </p>
      <p class="subtitle">
        The only sneaker site you would ever need.
      </p>

    </div>

   </section>

   <div class="colums is-multiline">
    <div class="column is-12">
      <h2 class="is-size-2 has-text-centered">Latest Sneakers</h2>
    </div>
   </div>

   <ProductBox 
   v-for="product in latestProducts"
   v-bind:key="product.id"
   v-bind:product="product" />

  </div>
</template>

<script>
import axios from 'axios'
import ProductBox from '@/components/ProductBox'

export default {
  name: 'Home',
  data() {
    return{
      latestProducts: []
    }
  },
  components: {
   ProductBox
  },
  mounted() {
  this.getLatestProducts()
  },
  methods: {
    getLatestProducts() {
    axios
      .get('/api/v1/latest-products/')
      .then(response => {
        this.latestProducts = response.data
      })
      .catch(error => {
        console.log(error)
      })
  }
}}
</script>



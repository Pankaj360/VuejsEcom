<template>
    <div class="createProduct">
        <modal :header="'Create Product'" :isShow="showModal" v-if="showModal" @close="showModal = false">
            <product-form :product="product" v-on:submit-form="productAction"/>
       </modal>
    </div>
</template>
<script>
import Modal from '../../shared/Modal.vue'
// eslint-disable-next-line no-unused-vars
import axios from 'axios'
import ProductForm from './ProductForm'
export default {
  name: 'createProduct',
  components: { Modal, ProductForm },
  data () {
    return {
      product: {},
      showModal: false
    }
  },
  methods: {
    showModalForm: function () {
      this.showModal = true
    },

    productAction: function (product) {
      this.data = true
      const product2 = {
        product: this.product
      }

      axios
        .post(`${process.env.VUE_APP_BASE_URL}/products`, product2)
        .then(response => {
          this.showLoader = false
          this.productAction(response.data[0])
          event.target.reset()
          this.$router.push(this.$route.query.from || '/')
        })
        .catch(error => {
          this.showLoader = false
          // eslint-disable-next-line no-undef
          errorToaster('add products', '')
          console.log(error)
        })
    }
  }
}
</script>
<style lang="scss">
</style>

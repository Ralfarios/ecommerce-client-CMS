<template>
  <main
    class="col-md-9 col-lg-10 px-md-4"
    style="margin-left: auto; margin-right: auto"
  >
    <div
      class="d-flex justify-content-between flex-wrap flex-md-nowrap align-items-center pt-3 pb-2 mb-3 border-bottom"
    >
      <h1 class="h2">Products</h1>
      <div class="btn-toolbar mb-2 mb-md-0">
        <router-link to="/admindashboard/products/add" style="text-decoration: none">
          <button type="button" class="btn btn-sm btn-outline-secondary">
            Add Product
          </button>
        </router-link>
      </div>
    </div>

    <router-view> </router-view>

    <div class="container-fluid">
      <div class="row">
        <product-card
          v-for="Product in Products"
          :key="Product.id"
          :Product="Product"
        />
      </div>
    </div>
  </main>
</template>

<script>
import ProductCard from './ProductCard.vue'

export default {
  name: 'Products',
  components: {
    ProductCard
  },
  methods: {
    fetchProducts () {
      this.$store.dispatch('fetchProducts')
    }
  },
  computed: {
    Products () {
      return this.$store.state.product.products
    }
  },
  created () {
    this.fetchProducts()
  }
}
</script>

<template>
  <div>
    <h1>Edit Product</h1>
    <form @submit.prevent="updateSubmit">
      <input
        v-model="Product.id"
        type="text"
        class="form-control"
        id="id"
        style="display: none"
      />

      <div class="mb-1">
        <label for="name" class="col-form-label">Game Title</label>
        <input
          v-model="Product.name"
          type="text"
          class="form-control"
          id="name"
        />
      </div>
      <div class="mb-1">
        <label for="image_url" class="col-form-label">Image URL</label>
        <input
          v-model="Product.image_url"
          type="text"
          class="form-control"
          id="image_url"
        />
      </div>

      <div class="row mb-1">
        <div class="col-6">
          <label for="price" class="col-form-label">Price</label>
          <div class="input-group">
            <div class="input-group-text">Rp.</div>
            <input
              v-model="Product.price"
              type="number"
              class="form-control"
              id="price"
            />
          </div>
        </div>
        <div class="col-6">
          <label for="stock" class="col-form-label">Stock</label>
          <input
            v-model="Product.stock"
            type="number"
            class="form-control"
            id="stock"
          />
        </div>
      </div>
      <label for="category" class="col-form-label">Category</label>
      <select
        v-model="Product.CategoryId"
        class="form-select"
        aria-label="Default select example"
      >
        <option value="">-- SELECT CATEGORY --</option>
        <option
          v-for="Category in Categories"
          :key="Category.id"
          :value="Category.id"
        >
          {{ Category.name }}
        </option>
      </select>

      <div class="mt-3 mb-3">
        <button type="submit" class="btn btn-sm btn-primary">Edit</button>
        <router-link to="/admindashboard/products" style="text-decoration: none">
          <button
            type="button"
            style="margin-left: 36px"
            class="btn btn-sm btn-danger"
          >
            Cancel
          </button>
        </router-link>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: 'EditProduct',
  data () {
    return {
      payload: {
        id: '',
        name: '',
        image_url: '',
        price: '',
        stock: '',
        CategoryId: ''
      }
    }
  },
  methods: {
    updateProduct () {
      this.$store.dispatch('updateProduct', this.payload)
    },
    fetchOneProduct () {
      this.$store.dispatch('fetchOneProduct', this.$route.params.id)
    },
    fetchCategories () {
      this.$store.dispatch('fetchCategories')
    },
    updateSubmit () {
      this.payload.id = this.Product.id
      this.payload.name = this.Product.name
      this.payload.image_url = this.Product.image_url
      this.payload.price = this.Product.price
      this.payload.stock = this.Product.stock
      this.payload.CategoryId = this.Product.CategoryId

      this.updateProduct()
    }
  },
  computed: {
    Categories () {
      return this.$store.state.category.categories
    },
    Product () {
      return this.$store.state.product.product
    }
  },
  created () {
    this.fetchCategories()
    this.fetchOneProduct()
  }
}
</script>

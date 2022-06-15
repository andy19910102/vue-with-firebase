<script setup>
import moment from "moment";
</script>

<template>
  <div class="card my-3">
    <img :src="product.image" class="card-img" />
    <div v-if="!editMode" class="card-body">
      <h5 class="card-title">{{ product.name }}</h5>
      <p class="card-text mb-2">$ {{ product.price }} NTD</p>
      <p class="card-text">
        <small>Created at {{ createdAt }}</small
        ><br />
        <small>Updated at {{ updatedAt }}</small>
      </p>
      <div>
        <button
          v-if="showEditSwitch"
          @click="turnEditMode"
          class="btn btn-warning"
        >
          Edit Mode
        </button>
      </div>
    </div>
    <form v-if="editMode" @submit.prevent="updateProduct" class="card-body">
      <div class="form-group">
        <input
          type="text"
          class="form-control"
          placeholder="Product Name"
          v-model="productName"
          required
        />
      </div>
      <div class="form-group">
        <input
          type="number"
          class="form-control"
          placeholder="Product Price"
          v-model="productPrice"
          required
        />
      </div>
      <div class="form-group">
        <input
          type="url"
          class="form-control"
          placeholder="Product Image URL"
          v-model="productImage"
          required
        />
      </div>
      <div class="form-group">
        <button type="submit" class="btn btn-warning mr-3">
          Update Product
        </button>
        <button type="button" @click="editMode = false" class="btn btn-light">
          Cancel
        </button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: "ProductCard",
  props: ["product", "showEditSwitch"],
  data() {
    return {
      editMode: false,
      productName: "",
      productPrice: 0,
      productImage: "",
    };
  },
  computed: {
    createdAt() {
      return moment(this.product.createdAt).format("YYYY/MM/DD HH:mm:ss");
    },
    updatedAt() {
      return moment(this.product.updatedAt).format("YYYY/MM/DD HH:mm:ss");
    },
  },
  methods: {
    turnEditMode() {
      (this.editMode = true), (this.productName = this.product.name);
      this.productPrice = this.product.price;
      this.productImage = this.product.image;
    },
    updateProduct() {
      const now = new Date().getTime();
      const updateProduct = {
        name: this.productName,
        price: this.productPrice,
        image: this.productImage,
        updatedAt: now,
      };
      this.$emit("update-product", {
        updateProduct,
        productId: this.product.id,
      });
    },
  },
};
</script>
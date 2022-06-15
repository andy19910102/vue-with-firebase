<script setup>
import { db } from "../firebase";
import {
  collection,
  doc,
  addDoc,
  getDocs,
  onSnapshot,
  updateDoc,
  orderBy,
} from "firebase/firestore";
import ProductCard from "../components/ProductCard.vue";
</script>

<template>
  <div class="row">
    <!-- new product -->
    <div class="col-md-4">
      <div class="card">
        <img :src="productImage" class="card-img" />
        <form @submit.prevent="createProduct" class="card-body">
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
            <button class="btn btn-success">Create Product</button>
          </div>
        </form>
      </div>
    </div>
    <!-- new product end -->
  </div>
  <div class="row">
    <!-- product list -->
    <div class="col-md-4">
      <ProductCard
        @update-product="updateProduct"
        :product="demoProduct"
        :showEditSwitch="true"
      />
    </div>
    <!-- product list end -->
  </div>
</template>

<script>
export default {
  name: "HomeView",
  data() {
    return {
      productList: [],
      productName: "Product A",
      productPrice: 499,
      productImage: "https://picsum.photos/id/157/1000/500",
      demoProduct: {
        id: "12345",
        name: "Product 1",
        price: 550,
        image: "https://picsum.photos/id/679/1000/500",
        createdAt: 1655272074015,
        updatedAt: 1655278094015,
      },
    };
  },
  methods: {
    createProduct() {
      const now = new Date().getTime();
      const product = {
        name: this.productName,
        price: this.productPrice,
        image: this.productImage,
        createdAt: now,
        updatedAt: now,
      };
      console.log("product", product);
    },
    updateProduct(data) {
      const { updateProduct, productId } = data;
      console.log("productId", productId);
      console.log("updateProduct", updateProduct);
    },
  },
  mounted() {
    console.log("mounted");
  },
};
</script>

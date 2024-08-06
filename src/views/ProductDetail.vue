<template>

<v-container class="pa-4">
  <v-btn
    @click="router.push({ name: 'Catalog' })"
    color="primary"
    variant="elevated"
    class="mb-4"
  >
    Back to catalog
  </v-btn>

  <v-card class="product" outlined>
    <v-row>
      <v-col cols="12" md="4" class="d-flex justify-center">
        <v-img :src="selectedProduct.thumbnail" alt="" max-height="200px" class="rounded"></v-img>
      </v-col>
      <v-col cols="12" md="4">
        <v-card-title class="headline">{{ selectedProduct.brand }}</v-card-title>
        <v-card-subtitle class="grey--text">{{ selectedProduct.description }}</v-card-subtitle>
        <v-divider class="my-3"></v-divider>
        <h2 class="subtitle-1 mb-3">Price: ₦ {{ (selectedProduct.price * 750).toFixed(2) }}</h2>
        <v-btn
          variant="elevated"
          color="indigo lighten-2"
          @click="addToCart"
        >
          Add to cart
        </v-btn>
      </v-col>
    </v-row>
  </v-card>
</v-container>

</template>


<script>
  import { defineComponent } from "vue";
  export default defineComponent({
    name: 'ProductDetails'
  })
</script>

<script setup>
  import { computed } from "vue";
  import { productsStore } from "@/stores/products";
  import { useRoute, useRouter } from "vue-router";

  const store = productsStore()
  const router = useRouter()
  const route = useRoute()

  const selectedProduct = computed(() => {
    return store.products.find((item) => item.id === Number(route.params.id))
  })

  const addToCart = () => {
    store.addToCart(selectedProduct.value)
    router.push({ name: 'CartView' })
  }
</script>

<style scoped>
.product {
  display: flex;
  margin-top: 50px;
}

.product-image {
  margin-right: 24px;
}

</style>
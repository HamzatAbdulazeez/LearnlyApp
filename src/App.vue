<template>
  <header class="pa-0">
    <v-toolbar title="Vue Test Application By Hamzat">
      <v-btn
          @click="router.push({ name: 'CartView' })"
          color="primary"
          variant="elevated"

      >Items in Cart: {{ store.cart.length }}
      </v-btn>
    </v-toolbar>
  </header>
  <main>
    <RouterView />
  </main>
</template>

<script setup>
  import { useRouter } from "vue-router";
  import { productsStore } from "@/stores/products";

  const router = useRouter()
  const store = productsStore()
</script>


<style scoped>
.cart-items {
  padding: 16px;
  font-weight: bold;
  font-size: 24px;
  cursor: pointer;
}
</style>

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

  <div v-if="!store.cart.length" class="text-center">
    <h1 class="display-1">Empty Cart ...</h1>
  </div>

  <div v-else>
    <v-row class="cart-items">
      <v-col
        v-for="item in store.cart"
        :key="item.id"
        cols="12"
        md="6"
        lg="4"
      >
        <v-card class="cart-item pa-3" outlined>
          <v-img :src="item.thumbnail" height="200px" class="rounded-t" cover></v-img>
          <v-card-title class="headline">{{ item.brand }}</v-card-title>
          <v-card-subtitle class="grey--text">{{ item.category }}</v-card-subtitle>
          <v-divider class="my-2"></v-divider>
          <v-card-text class="subtitle-1 mb-3">Price: ₦{{ (item.price * 750).toFixed(2) }}</v-card-text>
          <v-card-actions class="d-flex justify-end">
            <v-btn color="red" @click="removeFromCart(item.id)">
              Remove
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </div>
</v-container>

</template>

<script>
  import { defineComponent } from "vue";
  export default defineComponent({
    name: 'CartView'
  })
</script>

<script setup>
  import { productsStore } from "@/stores/products";
  import { useRouter } from "vue-router";

  const router = useRouter()

  const store = productsStore()

  const removeFromCart = (id) => {
    store.removeFromCart(id)
  }

</script>

<style scoped>
.item-details {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 32px;
  box-shadow: 0 0 17px 6px #e7e7e7;
  border-radius: 8px;
  padding: 16px;
}

.item-details img {
  width: 20%;
}
</style>
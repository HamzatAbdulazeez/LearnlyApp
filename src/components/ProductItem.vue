<template>
  <v-sheet class="ma-3 d-flex justify-center">
    <v-card class="product" outlined elevation="2">
      <v-img
        :src="props.productData.thumbnail"
        height="200px"
        class="rounded-t"
        cover
      ></v-img>

      <v-card-title class="headline text-center">
        {{ props.productData.brand }}
      </v-card-title>
      <v-card-subtitle class="text-center grey--text">
        ₦ {{ (props.productData.price * 750).toFixed(2) }}
      </v-card-subtitle>

      <v-card-text class="body-2 grey--text text--darken-1">
        {{ props.productData.description }}
      </v-card-text>

      <v-divider class="my-2"></v-divider>

      <v-card-actions class="d-flex justify-center">
        <v-btn color="primary" @click="goToProductPage(props.productData.id)">
          Add to Cart
        </v-btn>
      </v-card-actions>
    </v-card>
  </v-sheet>
</template>

<script>
import { defineComponent } from "vue";
export default defineComponent({
  name: "ProductItem",
});
</script>

<script setup>
import { defineProps, defineEmits } from "vue";
const props = defineProps({
  productData: {
    type: Object,
    required: true,
  },
});

const emit = defineEmits(["item-clicked"]);

const goToProductPage = (productId) => {
  emit("item-clicked", productId);
};
</script>

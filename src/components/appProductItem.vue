<template>
  <div class="product">
    <div class="left">
      <img class="product-img" :src="product.image" alt="" />
      <div class="product-info">
        <h1 class="product-title">{{ product.title }}</h1>
        <span class="product-price">₺{{ product.price.toFixed(2) }}</span>
      </div>
    </div>
    <button v-if="isPurchasedProduct(product.id) == false" @click="handleBuy">
      Buy
    </button>
    <button v-else @click="handleSell" class="red">Sell</button>
  </div>
</template>

<script setup>
import { defineProps, defineEmits } from "vue";
const { product } = defineProps({
  product: Object,
  isPurchasedProduct: Function,
});
const emit = defineEmits(["purchaseProductById", "sellProductById"]);
const handleBuy = () => {
  emit("purchaseProductById", product);
};
const handleSell = () => {
  emit("sellProductById", {
    id: product.id,
    price: product.price,
  });
};
</script>

<style scoped>
.product {
  width: 100%;
  max-width: 300px;
  padding: 12px 20px;
  background-color: white;
  border-radius: 12px;
  /* flex */
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.product .left {
  display: flex;
  align-items: center;
  gap: 12px;
  justify-content: center;
}
.product .product-img {
  width: 50px;
  height: 50px;
  border-radius: 50px;
  object-fit: cover;
}
.product .product-info {
  display: flex;
  gap: 6px;
  flex-direction: column;
}
.product .product-info > .product-title {
  font-size: 18px;
  font-weight: bold;
}
.product .product-info > .product-price {
  font-size: 14px;
  font-weight: 400;
}
.product button {
  width: 53px;
  height: 30px;
  border-radius: 5px;
  cursor: pointer;
  background-color: rgb(91, 91, 223);
  color: white;
  transition: all 75ms;
}
.product button:active {
  transition: all 75ms;
  background-color: rgb(91, 91, 223, 0.7);
}
.product button.red {
  background-color: rgb(255, 0, 0);
}
.product button.red:active {
  background-color: rgb(255, 0, 0, 0.7) !important;
}
</style>
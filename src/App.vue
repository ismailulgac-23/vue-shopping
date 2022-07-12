<template>
  <div id="wrapper">
    <div class="header">
      <h1 class="main-title">
        Alışveriş Sepeti Uygulaması - {{ wallet.toFixed(2) }} ₺
      </h1>
      <p class="purchased-count-text">
        Şuanda toplam <strong>{{ purchasedProducts.length }}</strong> kadar ürün
        satın aldınız..
      </p>
      <button @click="addMoneyToWallet">PARA EKLE +5₺</button>
    </div>
    <div class="product-list">
      <app-product-item
        v-for="product in products"
        :key="product.id"
        :product="product"
        @purchaseProductById="purchaseProductById"
        @sellProductById="sellProductById"
        :isPurchasedProduct="isPurchasedProduct"
      />
    </div>
  </div>
</template>
<script setup>
import { ref } from "vue";
import { products } from "@/constants/data";
import appProductItem from "./components/appProductItem.vue";

const wallet = ref(5.0);
const purchasedProducts = ref([]);

const purchaseProductById = (product) => {
  if (wallet.value >= product.price) {
    wallet.value -= product.price;
    purchasedProducts.value.push(product);
  } else {
    alert("Yeterli paranız yok lütfen cüzdanınıza para ekleyin");
  }
};
const sellProductById = ({ price, id }) => {
  wallet.value += price;
  purchasedProducts.value = purchasedProducts.value.filter(
    (purchasedProductItem) => purchasedProductItem.id != id
  );
};

const isPurchasedProduct = (id) => {
  const product = purchasedProducts.value.find(
    (purchasedProductItem) => purchasedProductItem.id == id
  );
  if (product) {
    return true;
  } else {
    return false;
  }
};

const addMoneyToWallet = () => (wallet.value += 5);
</script>


<style>
* {
  margin: 0px;
  padding: 0px;
  text-decoration: none;
  box-sizing: border-box;
  border: none;
  outline: none;
}
body {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif !important;
  background-color: #f1f1f1;
}
.header {
  margin-bottom: 22px;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}
.header button {
  width: auto;
  padding: 0px 12px;
  height: 30px;
  border-radius: 5px;
  cursor: pointer;
  background-color: rgb(91, 91, 223);
  color: white;
  transition: all 75ms;
}
.header button:active {
  transition: all 75ms;
  background-color: rgb(91, 91, 223, 0.7);
}
.main-title {
  font-size: 42px;
}
.purchased-count-text {
  margin: 12px 0px;
}
#wrapper {
  padding-top: 100px;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}
.product-list {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 12px;
  flex-wrap: wrap;
}
</style>
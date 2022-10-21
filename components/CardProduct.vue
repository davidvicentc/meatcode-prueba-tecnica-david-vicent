<template>
  <v-col cols="6" md="4">
    <v-card class="mx-auto card-product" max-width="344">
      <v-img :src="product.image" height="200px"></v-img>
      <v-card-title class="card-title">{{ product.title }}</v-card-title>
      <v-card-subtitle>{{ product.content }}</v-card-subtitle>
    </v-card>
  </v-col>
</template>

<script>
export default {
  props: ["product"],
};
</script>

<style>
.card-title {
  font-family: "Open Sans";
  font-weight: 700;
  font-size: 18px;
  line-height: 24px;
  margin-bottom: 15px;
  margin-top: 15px;
}

.card-product {
  border-radius: 10px 10px 10px 10px !important;
  box-shadow: 0px -2px 0px -2px rgb(0 0 0 / 20%),
    0px 2px 2px 0px rgb(0 0 0 / 3%), 0px 1px 5px 0px rgb(0 0 0 / 6%) !important;
  height: 438px;
}
</style>

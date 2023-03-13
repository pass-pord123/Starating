<template>
  <div v-for="(item, index) in products" :key="index">
    <HelloWorld :name="item.product" v-model="item.star" />
    <textarea name="" id="" cols="60" rows="10" v-model="item.text"> </textarea>
     <hr />
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
export default {
  name: "App",
  components: {
    HelloWorld,
  },
  data() {
    return {
      products: [
        { product: "Huawei", star: 5, text: "input your comment" },
        { product: "Samsung", star: 3, text: "input your comment" },
        { product: "Vivo", star: 4, text: "input your comment" },
        { product: "Oppo", star: 2, text: "" },
      ],
    };
  },
};
</script>

<style></style>

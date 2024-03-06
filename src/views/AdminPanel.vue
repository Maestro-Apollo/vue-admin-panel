<template>
  <div>
    <table border="1">
      <thead>
      <tr>
        <th>ID</th>
        <th>Title</th>
        <th>Price</th>
        <th>Description</th>
        <th>Thumbnail</th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="product in products" :key="product.id">
        <td>{{ product.id }}</td>
        <td>{{ product.title }}</td>
        <td>{{ product.price }}</td>
        <td>{{ product.description }}</td>
        <td><img :src="product.thumbnail" alt=""></td>
      </tr>
      </tbody>
    </table>
  </div>
</template>


<script>
import { ref, onMounted } from 'vue';
import axios from 'axios';


export default {
  name: 'AdminPanel',
  setup() {
    const products = ref([]);


    async function fetchProducts() {
      const response = await axios.get('https://dummyjson.com/products');
      products.value = response.data.products;
      console.log(products.value);
      console.log(response, response.data);
    }


    onMounted(fetchProducts);


    return {
      products
    };
  }
};
</script>

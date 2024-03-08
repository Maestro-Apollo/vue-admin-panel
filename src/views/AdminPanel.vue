<template>
  <div>

    <input type="text" v-model="search" placeholder="Search...">
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
      <tr v-for="product in filterMethod" :key="product.id">
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
import {ref, onMounted, computed} from 'vue';
import axios from 'axios';


export default {
  name: 'AdminPanel',
  setup() {
    const products = ref([]);
    const search = ref('');

    async function fetchProducts() {
      const response = await axios.get('https://dummyjson.com/products');
      products.value = response.data.products;
    }
    onMounted(fetchProducts);
    const filterMethod = computed(()=>{
      return products.value.filter((product)=>product.title.toLowerCase().includes(search.value.toLowerCase()));
    })
    return {
      products,
      search,
      filterMethod
    };
  }
};
</script>

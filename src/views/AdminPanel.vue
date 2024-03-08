<template>
  <v-container>
    <v-text-field v-model="search" label="Search" outlined></v-text-field>
    <v-data-table
        :headers="headers"
        :items="filterMethod"
        item-key="id"
        :search="search"
    >
      <template v-slot:item.thumbnail="{ item }">
        <v-img :src="item.thumbnail" width="100" height="100"></v-img>
      </template>
      <template v-slot:thead>
        <thead>
        <tr>
          <th v-for="header in headers" :key="header.text">{{ header.text }}</th>
        </tr>
        </thead>
      </template>
    </v-data-table>
  </v-container>
</template>

<script>
import { ref, onMounted, computed } from 'vue';
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

    const headers = [
      { text: 'ID', value: 'id' },
      { text: 'Title', value: 'title' },
      { text: 'Price', value: 'price' },
      { text: 'Description', value: 'description' },
      { text: 'Thumbnail', value: 'thumbnail' }
    ];

    const filterMethod = computed(() =>
        products.value.filter((product) =>
            product.title.toLowerCase().includes(search.value.toLowerCase())
        )
    );

    return {
      headers,
      products,
      search,
      filterMethod
    };
  }
};
</script>

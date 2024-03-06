<template>
  <div>
    <input type="text" v-model="newItemText" placeholder="Add new item">
    <button @click="addItem">Add</button>
    <ul>
      <li v-for="(item, index) in items" :key="index">
        {{ item }}
        <button @click="editItem(index)">Edit</button>
        <button @click="deleteItem(index)">Delete</button>
      </li>
    </ul>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  name: "crud",
  setup() {
    const items = ref(['Item 1', 'Item 2', 'Item 3']);
    const newItemText = ref('');

    function addItem() {
      if (newItemText.value.trim() !== '') {
        items.value.push(newItemText.value.trim());
        newItemText.value = '';
      }
    }

    function editItem(index) {
      const newText = prompt('Enter new text:', items.value[index]);
      if (newText !== null) {
        items.value[index] = newText;
      }
    }

    function deleteItem(index) {
      if (confirm('Are you sure you want to delete this item?')) {
        items.value.splice(index, 1);
      }
    }

    return {
      items,
      newItemText,
      addItem,
      editItem,
      deleteItem
    };
  }
};
</script>

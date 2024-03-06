<template>
  <div class="home">
    <h1>Home</h1>
    <h2>Refs</h2>
    <p>{{ninjaOne.age}}</p>
    <p>{{ninjaTwo.age}}</p>
    <button @click="updateNinjaOne">Click to Update N1</button>
    <button @click="updateNinjaTwo">Click to Update N2</button>
    <input type="text" v-model="search">

    <div v-for="name in filterMethod" :key="name">
      <p>{{name}}</p>
    </div>

  </div>
</template>

<script>
// @ is an alias to /src

import {ref, reactive, computed} from "vue";

export default {
  name: 'HomeView',
  setup(){

    const names = ref(['Rafi', 'Mahafid', 'Edward', 'Elric']);

    const search = ref("");

    const ninjaOne = ref({name: 'mario', age:30});
    const ninjaTwo = reactive({name: 'rafi', age:35});
    const updateNinjaOne = () =>{
      ninjaOne.value.age = 40;
    }
    const updateNinjaTwo = () =>{
      ninjaTwo.age = 46;
    }
    const filterMethod = computed(()=>{
        return names.value.filter((name)=>name.includes(search.value));
    })

    return {updateNinjaOne, ninjaOne, ninjaTwo, updateNinjaTwo, names, search, filterMethod}
  },
  created() {
  },
  mounted() {
  }
}
</script>

|<template>
        
       region:
    <select v-model="selecteRegion">
     <option v-for="item in regionItems" :key="item" >
      {{ item }}
    </option>
    </select> 
    <ul>
          <li v-for="item in visibleCountries" :key="item.cca3">
    
            <img class="flag" :src="item.flags.png" :alt="item.flags.alt">
            <NuxtLink :to="{
              name: 'country-iata',
              params: {
                   iata: item.cca3
                }
            }">{{ item.name.common }}</NuxtLink>
    
          </li>
        </ul>
    </template>

    <script setup>
    import { ref ,computed} from 'vue'
  const countries = ref([])
  const selecteRegion=ref(null)


  const getCountries = async (query) => {
    const url = query ? `https://restcountries.com/v3.1/name/${query}` : 'https://restcountries.com/v3.1/all'
    const response = await fetch(url);
    debugger;
    countries.value = await response.json();
  }

  getCountries()

  const regionItems = [
      'All',
      'Asia',
      'Europe',
      'Americas',
      'Africa',
      'Oceania',
      'Antarctic',
  ]
    
    const visibleCountries=computed(()=>{
  if(selecteRegion.value && selecteRegion.value!='All')
  {
    const res=countries.value.filter(item=>item.region===selecteRegion.value)
    return res;
  }

  return countries.value;
})
 
    </script>
    <style lang="postcss" scoped>
    ul {
      list-style: none;
      display: flex;
      flex-wrap: wrap;
      width: 100%;
      padding: 0;
  
      & li {
        flex-basis: calc(100% / 4);
        width: calc(100% / 4);
        padding: 12px;
      }
    }
  
  </style>
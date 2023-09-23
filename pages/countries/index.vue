<template>
    <card></card>
    <ul >
        <li v-for="country in countries" :key="country.name.common">
            <FlagCard :country="country"></FlagCard>
        </li>
    </ul>
</template>
<script setup>
const countries=ref([])
const getCountries = async () => {
    const url = 'https://restcountries.com/v3.1/all'
    const response = await fetch(url);
    debugger;
    countries.value = await response.json();
  }

  getCountries()
</script>

    

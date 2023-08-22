<script setup>

const route=useRoute();
const selectedCountry=ref('');
const selectedBorders=ref([]);

const getSelectedCountry = async (title) => {
    debugger
const url =  `https://restcountries.com/v3.1/alpha/${title}`
    // const url =  `https://restcountries.com/v3.1/name/${title}?fullText=true`
    const response = await fetch(url);
    const selectedCountries = await response.json();
    selectedCountry.value = selectedCountries[0];


    const borderCodes=selectedCountry.value.borders.join(','); 
    const codeUrl =  `https://restcountries.com/v3.1/alpha?codes=${borderCodes}`
    const borderResponse = await fetch(codeUrl);
    selectedBorders.value = await borderResponse.json();

 
  }


if(!!route.params.iata)
{
    getSelectedCountry(route.params.iata);
}

</script>

<template>
   <div v-if="!!selectedCountry">

      {{ selectedCountry.name.common }}
      <img class="flag" :src="selectedCountry.flags.png" :alt="selectedCountry.flags.alt">

      <ul>
        <li v-for="border in selectedBorders" :key="border">

          {{ border.name.common }}
          <!-- <img class="flag" :src="border.flags.png" :alt="border.flags.alt"> -->
          <NuxtLink :to="{
              name: 'country-iata',
              params: {
                   iata: border.cca3
                }
            }">{{ border.name.common }}</NuxtLink>

        </li>
      </ul>
  </div>
</template>
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
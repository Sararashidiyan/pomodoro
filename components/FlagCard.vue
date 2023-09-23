<template>
    <div>
      <img class="h-10 w-10 rounded-full" :src="country.flags.png" alt="country.flags.alt" />
      <div class="ml-3">
        <p class="text-sm font-medium text-gray-900">{{ country.name.common }}</p>
      </div>
    </div>
</template>
<script setup>
  defineProps({
    country: {
        type: Object
      }
    })
</script>

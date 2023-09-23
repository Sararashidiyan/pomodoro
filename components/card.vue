<template>
    <component :is="tag" class="bg-white rounded-2xl p-4">
      <slot/>
    </component>
  </template>
  <script setup>
    defineProps({
      tag: {
        type: String,
        default: 'div'
      }
    })
  </script>
  <style lang="pcss" scopped>
    
  </style>
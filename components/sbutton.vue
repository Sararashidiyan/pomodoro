<template>
    <button @click="emit('onClick')" :class="type">{{ content }}</button>
</template>
<script setup>
    import { string, oneOf, bool, number } from 'vue-types'
const props = defineProps({
  content: string(),
  type:oneOf(['primary', 'secondary']).def('primary')
})
const emit = defineEmits(['onClick'])
</script>
<style scoped>
.primary{
    @apply bg-black font-medium  text-slate-50 py-2 px-4 rounded-full w-80 my-3
}
.secondary{
    @apply bg-gray-300 font-medium text-current py-2 px-4 rounded-full w-80 my-3
}
</style>

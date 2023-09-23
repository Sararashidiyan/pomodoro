<template>
    <input @blur="validateInput" v-model="localModelValue" :type="type" :id="id" class="w-80 bg-white border border-gray-500 bg-slate-400 placeholder-bg-slate-300 text-sm rounded-lg block w-full p-2.5 dark:bg-gray-700 dark:border-gray-500" :placeholder="placeholder">
    <span class="input-description">{{description}}</span>
    <br/>
    <span class="error-msg">{{validateEmailMsg}}</span>
</template>
<script setup>
import { string, oneOfType, bool, number } from 'vue-types'
const props = defineProps({
    label: string(),
    description: string(),
    placeholder: string(),
    id: string(),
    name: string(),
    type: string().def('text'),
    modelValue: oneOfType([string(), number()]),
  })
  const emit = defineEmits(['valid'])
  const { localModelValue} = useLocalModelValue({ props})
  const validateEmailMsg=ref('')
  const validateInput=()=> {
    const value=localModelValue.value;
    if(props.type=='Email')
    {
    if (!(/^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/.test(value))) {
        debugger;
        validateEmailMsg.value = 'Please enter a valid email address';
        emit('validate',false)
    } else {
        validateEmailMsg.value = '';
        emit('validate',true)
    }
    }
   
}
</script>
<style scoped>
.input-description{
    @apply text-gray-300 font-normal text-sm
}
.error-msg{
    @apply text-red-600 font-normal text-sm
}
</style>

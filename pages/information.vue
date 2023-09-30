<template>
    name:
<input v-bind="nameModel"/>
{{ errors.name }}
<br/>
phone:
<input v-bind="phoneModel"/>
{{ errors.phone }}
<br/>
email:
<input v-bind="emailModel"/>
{{ errors.email }}
</template>
<script setup>
    import * as yup from 'yup';
    import { useForm} from 'vee-validate';
    let userSchema = yup.object({
  name: yup.string().required().test((value,context)=>{return isNameValid(value) || context.createError({message:'name is not valid'})  }),
  email: yup.string().required().test((value,context)=>{return isEmailValid(value) || context.createError({message:'email is not valid'})  }),
  phone:yup.string().required().test((value,context) =>{return isIrainianPhone(value) || context.createError({message:'phoe is not valid'})})
});
const isIrainianPhone=(value)  =>{
    debugger;
    const reg = new RegExp("^09[0|1|2|3][0-9]{8}$");
    return reg.test(value);
}
const isEmailValid=(value)  =>{
    debugger;
    const reg = new RegExp("/^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/");
    return reg.test(value);
}
const isNameValid=(value)  =>{
    debugger;
return value.lenght>2 && value.lenght<255
}

const {defineInputBinds,errors}=useForm({validationSchema:userSchema}) 
const emailModel=defineInputBinds('email')
const nameModel=defineInputBinds('name')
const phoneModel=defineInputBinds('phone')
</script>

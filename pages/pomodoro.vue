<template>
    <div class="flex h-screen">
        <div class="bg-zinc-300 w-1/3" >
            <button @click="showFormFunc()">salam</button>
            <p>{{ counter }}</p>
        </div>
       <div v-show="showForm" class="w-2/3 grid grid-rows-5 grid-flow-col gap-2 grid-cols-3 gap-2 my-3">
        <div  class="col-start-3 flex justify-around">
            <label >statistic</label>
            <label >profile</label>
        </div>
        <div class="row-span-3 row-start-2 col-start-2">
            <label class="font-bold">New Task</label>
            <sput v-model="name" description="task description" name="name" id="nameId" placeholder="Enter Name"/>
            <sput v-model="email" type="Email" @validate="validateEmail($event)" description="email" name="email" id="emailId" placeholder="Enter Email"/>
            <br/>
            <sbutton  @onClick="saveClick()" type="primary" content="start"/>
            <br/>
            <sbutton @onClick="cancelClick()" type="secondary" content="cancel"/>
        </div>
        <div class="col-start-1 col-span-3 flex justify-around row-start-5">
            <label>Today</label>
            <label>Week</label>
            <label>Month</label>
        </div>
       </div>
    </div>
</template>
<script setup>
const name =ref('') 
const email =ref('') 
const counter=ref(20)
const saveButtonIsInvalid=ref(true)
const showForm=ref(false)
const showFormFunc =()=>{
    showForm.value=true;
}
 const validateEmail =(value)=>{
        saveButtonIsInvalid.value=value;
}

const saveClick =()=>{
    setInterval(() => {
        if(counter.value>0){
        counter.value=counter.value-1
        }
  }, 2000)
}
const cancelClick=function(){
    showForm.value=false;
}
</script>

<template>
    <CollectionTest3List  @openAddModal="openAddModal" @editDetails="editDetailsModal" :people="peopleList" :key="render" @deleteDetails="deleteDetails" />
    <CollectionTest3Add :openAddDetailsModal="openAddDetailsModal" @addDetails="addDetails" />
    <CollectionTest3Edit :editDetails="editDetails" :openEditDetailsModal="openEditDetailsModal" @updateDetails="updateDetails" />
</template>
<script lang="ts" setup>

import {ref} from "vue";

const openAddDetailsModal=ref(false);
const openEditDetailsModal=ref(false);
const editDetails=ref({})
const render=ref(0);
const index=ref(0);

const peopleList = ref([]);

const openAddModal =()=>{
    openAddDetailsModal.value=true
}

const editDetailsModal =(data:any,index:any) =>{
    openEditDetailsModal.value=true;
    editDetails.value=data;
    index.value=index
}

const updateDetails =(data:any) =>{
    openEditDetailsModal.value=false
}
 
onMounted(() =>{
    const items = localStorage.getItem("peopleList"); 
    peopleList.value=JSON.parse(items)
});

const deleteDetails =(data:any) =>{
    peopleList.value.splice(data, 1);
  localStorage.setItem("peopleList", JSON.stringify(peopleList.value)); 
}

const addDetails =(data:any) =>{
 peopleList.value.push(data)
 localStorage.setItem("peopleList", JSON.stringify(peopleList.value));
 openAddDetailsModal.value=false
 render.value++
}
</script>
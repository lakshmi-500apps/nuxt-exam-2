<template>
  <CollectionBuilderList
    :builderList="buildersList"
    @openModal="openModal"
    @editModal="openEditBuilderModal"
    @deleteBuilder="deleteBuilder"
  />
  <CollectionBuilderAdd
    :openBuilderModal="openAddModal"
    @addBuilderData="addBuilderData"
  />
  <CollectionBuilderEdit
    :openEditModal="openEditModal"
    :builderData="builderData"
    @updateBuilderData="addBuilderData"
  />
</template>
<script setup lang="ts">
import { ref } from "vue";

// Declaring Variables
const buildersList = ref([]);
const openAddModal = ref(false);
const openEditModal = ref(false);
const builderData = ref({});
const baseUrl = "https://v1-orm-gharpe.mercury.infinity-api.net/api/builder/";

const { data: items } = await useAuthLazyFetch(
  `${baseUrl}?offset=0&limit=100&sort_column=id&sort_direction=desc`,
  ""
);

buildersList.value = items.value;

// Open Add Builder Modal
const openModal = (data: any) => {
  openAddModal.value = true;
};

// Open Edit Builder Data Modal
const openEditBuilderModal = (data: any) => {
  (openEditModal.value = true), (builderData.value = data);
};

// Add or Update Builder data
const addBuilderData = async (data: any) => {
  if (data.uid) {
    const putoptions = {
      body: data,
    };
    await useAuthLazyFetchPut(`${baseUrl}${data.uid}`, putoptions);
    openEditModal.value = false;
    // Update QuestionsList Data after inserting a new value
    const { data: response } = await useAuthLazyFetch(
      "https://v1-orm-gharpe.mercury.infinity-api.net/api/builder/?offset=0&limit=100&sort_column=id&sort_direction=desc",
      ""
    );
    buildersList.value = response.value;
  } else {
    const postoptions = {
      body: data,
    };
    await useAuthLazyFetchPost(baseUrl, postoptions);
    openAddModal.value = false;
    // Update QuestionsList Data after inserting a new value
    const { data: response } = await useAuthLazyFetch(
      "https://v1-orm-gharpe.mercury.infinity-api.net/api/builder/?offset=0&limit=100&sort_column=id&sort_direction=desc",
      ""
    );
    buildersList.value = response.value;
  }
};


// Delete Builder
const deleteBuilder = async (data: any) => {
  const deleteoptions = { body: data };
  await useAuthLazyFetchDelete(`${baseUrl}${data.uid}`, deleteoptions);

  const { data: response } = await useAuthLazyFetch(
    "https://v1-orm-gharpe.mercury.infinity-api.net/api/builder/?offset=0&limit=100&sort_column=id&sort_direction=desc",
    ""
  );
  buildersList.value = response.value;
};
</script>

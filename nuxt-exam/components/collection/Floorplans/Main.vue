<template>
  <CollectionFloorplansList
    :floorPlansData="floorPlansData"
    @openAddSidebar="openAddSidebar"
    @delete="deleteFloorplan"
    @openEditSidebar="openEditSidebar"
  />
  <CollectionFloorplansAdd :addSidebar="addSidebar" @formData="addFloorPlan" />
  <CollectionFloorplansEdit
    :editSidebar="editSidebar"
    :floorPlanData="floorPlanData"
    @formData="addFloorPlan"
  />
</template>
<script lang="ts" setup>
import { ref } from "vue";

const floorPlansData = ref([]);
const baseUrl =
  "https://v1-orm-gharpe.mercury.infinity-api.net/api/floorplans/";
const addSidebar = ref(false);
const editSidebar = ref(false);
const floorPlanData = ref({});

const { data: getFloorplans } = await useAuthLazyFetch(
  `${baseUrl}?offset=0&limit=100&sort_column=id&sort_direction=desc`,
  ""
);
floorPlansData.value = getFloorplans.value;

const openAddSidebar = () => {
  addSidebar.value = true;
};

const openEditSidebar = (data: any) => {
  editSidebar.value = true;
  floorPlanData.value = data;
};
const addFloorPlan = async (data: any) => {
  if (data.uid) {
    const putoptions = { body: data };
    await useAuthLazyFetchPut(`${baseUrl}${data.uid}`, putoptions);
    editSidebar.value = false;
    const { data: response } = await useAuthLazyFetch(
      `${baseUrl}?offset=0&limit=100&sort_column=id&sort_direction=desc`,
      ""
    );
    floorPlansData.value = response.value;
  } else {
    const postoptions = { body: data };
    await useAuthLazyFetchPost(`${baseUrl}`, postoptions);

    addSidebar.value = false;

    const { data: response } = await useAuthLazyFetch(
      `${baseUrl}?offset=0&limit=100&sort_column=id&sort_direction=desc`,
      ""
    );
    floorPlansData.value = response.value;
  }
};

const deleteFloorplan = async (data: any) => {
  const deleteoptions = { body: data };
  await useAuthLazyFetchDelete(`${baseUrl}${data.uid}`, deleteoptions);
  const { data: response } = await useAuthLazyFetch(
    `${baseUrl}?offset=0&limit=100&sort_column=id&sort_direction=desc`,
    ""
  );
  floorPlansData.value = response.value;
};
</script>

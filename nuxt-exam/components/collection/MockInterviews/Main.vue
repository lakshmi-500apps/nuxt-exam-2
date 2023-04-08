<template>
  <CollectionMockInterviewsList
    :getInterviews="getInterviews"
    @openModal="openMockModal"
    @openViewModal="openViewModal"
  />
  <CollectionMockInterviewsAdd :openModal="openModal" @addMock="addMock" />
  <CollectionMockInterviewsEdit
    :viewModal="viewModal"
    :viewMockInterviewDetails="viewMockInterviewDetails"
  />
</template>
<script setup lang="ts">
import { ref } from "vue";

// Defining of Variables
const getInterviews = ref([]);
const openModal = ref(false);
const viewModal = ref(false);
const viewMockInterviewDetails = ref({});

// To get Projects
const { data: items } = await useAuthLazyFetch(
  "https://v7-stark-db-orm.mercury.infinity-api.net/api/mock-interviews/?offset=0&limit=100&sort_column=id&sort_direction=desc",
  ""
);
getInterviews.value = items.value;

// Open Add MockInterview Modal
const openMockModal = () => {
  openModal.value = true;
};

// To newly add MockInterview
const addMock = async (data: any) => {
  const postoptions = {
    body: data,
  };
  await useAuthLazyFetchPost(
    "https://v7-stark-db-orm.mercury.infinity-api.net/api/mock-interviews/",
    postoptions
  );
  openModal.value = false;

  const { data: response } = await useAuthLazyFetch(
    "https://v7-stark-db-orm.mercury.infinity-api.net/api/mock-interviews/?offset=0&limit=100&sort_column=id&sort_direction=desc",
    ""
  );
  getInterviews.value = response.value;
};

// To preview on row click of selected interview
const openViewModal = (data: any) => {
  viewModal.value = true;
  viewMockInterviewDetails.value = data;
};
</script>

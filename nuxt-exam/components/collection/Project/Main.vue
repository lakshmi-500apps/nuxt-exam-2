<template>
  <!-- To show table Format of Projects -->
  <CollectionProjectList
    :getProjects="getProjects"
    @openAddProjectSidebar="openAddProject"
    @openEditProjectSidebar="updateProjectData"
    @deleteProject="deleteProject"
  />
  <!-- For Adding of Projects -->
  <CollectionProjectAdd
    :openAddProjectSidebar="openAddProjectSidebar"
    @formData="getProjectFormData"
    @cancel="cancel"
  />
  <!-- For Editing of Project Data -->
  <CollectionProjectEdit
    :openEditProjectSidebar="openEditProjectSidebar"
    :getProjectData="getProjectData"
    @formData="getProjectFormData"
    @cancel="cancel"
  />
</template>
<script setup lang="ts">
import { ref } from "vue";

// Defining of Variables
const getProjects = ref([]);
const openAddProjectSidebar = ref(false);
const openEditProjectSidebar = ref(false);
const getProjectData = ref({});

// To get Projects
const { data: items } = await useAuthLazyFetch(
  "https://v1-orm-gharpe.mercury.infinity-api.net/api/projects/?offset=0&limit=100&sort_column=id&sort_direction=desc",
  ""
);
getProjects.value = items.value;

// Open AddProject Sidebar From Empty state or Add Project Button
const openAddProject = () => {
  openAddProjectSidebar.value = true;
};

// To Add or Update Project Details
const getProjectFormData = async (data: any) => {
  if (data.uid) {
    const putoptions = { body: data };
    await useAuthLazyFetchPut(
      `https://v1-orm-gharpe.mercury.infinity-api.net/api/projects/${data.uid}`,
      putoptions
    );
    openEditProjectSidebar.value = false;

    const { data: response } = await useAuthLazyFetch(
      "https://v1-orm-gharpe.mercury.infinity-api.net/api/projects/?offset=0&limit=100&sort_column=id&sort_direction=desc",
      ""
    );
    getProjects.value = response.value;
  } else {
    const postoptions = {
      body: data,
    };
    await useAuthLazyFetchPost(
      "https://v1-orm-gharpe.mercury.infinity-api.net/api/projects/",
      postoptions
    );
    openAddProjectSidebar.value = false;

    const { data: response } = await useAuthLazyFetch(
      "https://v1-orm-gharpe.mercury.infinity-api.net/api/projects/?offset=0&limit=100&sort_column=id&sort_direction=desc",
      ""
    );
    getProjects.value = response.value;
  }
};

// Prefill the project Data and open Edit Project Sidebar
const updateProjectData = (data: any) => {
  openEditProjectSidebar.value = true;
  getProjectData.value = data;
};

// Delete Selected Project
const deleteProject = async (data: any) => {
  const deleteoptions = { body: data };
  await useAuthLazyFetchDelete(
    `https://v1-orm-gharpe.mercury.infinity-api.net/api/projects/${data.uid}`,
    deleteoptions
  );
  const { data: response } = await useAuthLazyFetch(
    "https://v1-orm-gharpe.mercury.infinity-api.net/api/projects/?offset=0&limit=100&sort_column=id&sort_direction=desc",
    ""
  );
  getProjects.value = response.value;
};

// Close Sidebar on clicking cancel button
const cancel = () => {
  openAddProjectSidebar.value = false;
  openEditProjectSidebar.value = false;
};
</script>

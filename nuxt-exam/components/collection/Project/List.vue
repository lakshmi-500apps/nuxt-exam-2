<template>
     <div class="px-4 sm:px-6 lg:px-8 border mt-5 ml-5 mr-7">
     <div class="sm:flex sm:items-center">
      <div class="sm:flex-auto">
        <h1 class="text-base font-semibold leading-6 text-gray-900">
        Projects
        </h1>
      </div>
      <div class="mt-4 sm:ml-16 sm:mt-0 sm:flex-none">
        <button
          type="button"
          @click="openAddSidebar"
          class="mt-2 block rounded-md bg-indigo-600 px-3 py-2 text-center text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
        >
          + Add Project
        </button>
      </div>
    </div>
  <!-- Table format starts here and this appears only if projects are present -->
  <div
    v-if="getProjects.length > 0"
    class="mt-8 flow-root mr-[4.75rem] ml-[4.25rem]"
  >
    <div class="-mx-4 -my-2 border overflow-x-auto sm:-mx-6 lg:-mx-8">
      <div class="inline-block min-w-full py-2 align-middle sm:px-6 lg:px-8">
        <table class="min-w-full divide-y divide-gray-300">
          <thead>
            <tr>
              <th
                scope="col"
                class="py-3.5 pl-4 pr-3 text-left text-sm font-semibold text-gray-900 sm:pl-0"
              >
                Name
              </th>
              <th
                scope="col"
                class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900"
              >
                Category
              </th>
              <th
                scope="col"
                class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900"
              >
                Sub Category
              </th>
              <th
                scope="col"
                class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900"
              >
                Status
              </th>
              <th
                scope="col"
                class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900"
              >
                Metric
              </th>
              <th
                scope="col"
                class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900"
              >
                Details
              </th>
              <th
                scope="col"
                class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900"
              >
                Total Project Area
              </th>
              <th
                scope="col"
                class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900"
              >
                Listing Type Name
              </th>
            </tr>
          </thead>
          <tbody class="divide-y divide-gray-200">
            <tr v-for="project in getProjects" :key="project.name">
              <td
                class="whitespace-nowrap py-4 pl-4 pr-3 text-sm font-medium text-gray-900 sm:pl-0"
              >
                {{ project.name }}
              </td>
              <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                {{ project.category }}
              </td>
              <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                {{ project.sub_category }}
              </td>
              <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                {{ project.status }}
              </td>
              <td
                class="whitespace-nowrap px-3 py-4 text-sm text-gray-500 truncate"
              >
                {{ project.metric }}
              </td>
              <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                {{ project.details }}
              </td>
              <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                {{ project.total_project_area }}
              </td>
              <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                {{ project.listing_type_name }}
              </td>
              <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                <div class="flex justify-between">
                  <div>
                    <PencilSquareIcon
                      class="h-5 w-5"
                      @click="openEditSidebar(project)"
                    />
                  </div>
                  <div>
                    <TrashIcon
                      class="h-5 w-5"
                      @click="deleteProject(project)"
                    />
                  </div>
                </div>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
  <!-- Empty State Starts here -->
  <div v-else>
    <div class="text-center py-6 mr-[31.75rem] ml-[36.25rem]">
      <svg
        class="mx-auto h-12 w-12 text-gray-400"
        fill="none"
        viewBox="0 0 24 24"
        stroke="currentColor"
        aria-hidden="true"
      >
        <path
          vector-effect="non-scaling-stroke"
          stroke-linecap="round"
          stroke-linejoin="round"
          stroke-width="2"
          d="M9 13h6m-3-3v6m-9 1V7a2 2 0 012-2h6l2 2h6a2 2 0 012 2v8a2 2 0 01-2 2H5a2 2 0 01-2-2z"
        />
      </svg>
      <h3 class="mt-2 text-sm font-semibold text-gray-900">No projects</h3>
      <p class="mt-1 text-sm text-gray-500">
        Get started by creating a new project.
      </p>
      <div class="mt-6">
        <button
          type="button"
          @click="openAddSidebar"
          class="inline-flex items-center rounded-md bg-indigo-600 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
        >
          <PlusIcon class="-ml-0.5 mr-1.5 h-5 w-5" aria-hidden="true" />
          New Project
        </button>
      </div>
    </div>
  </div>
</div>
  <!-- Empty State Ends here -->
</template>
<script setup lang="ts">
import { PlusIcon, PencilSquareIcon, TrashIcon } from "@heroicons/vue/20/solid";

// Define Props
const props = defineProps({
  getProjects: Array,
});

// Define Emits
const emit = defineEmits([
  "openAddProjectSidebar",
  "openEditProjectSidebar",
  "deleteProject",
]);

// Open Add Project Sidebar
const openAddSidebar = () => {
  emit("openAddProjectSidebar", true);
};

// Open Edit Project Sidebar

const openEditSidebar = (data: any) => {
  emit("openEditProjectSidebar", data, true);
};

// Delete Project
const deleteProject = (data: any) => {
  emit("deleteProject", data);
};
</script>

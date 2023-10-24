<template>
  <div class="px-4 sm:px-6 lg:px-8 border mt-5 ml-5 mr-7">
    <!-- Add MockInterview Form Starts Here -->
    <div class="sm:flex sm:items-center" v-if="getInterviews.length>0">
      <div class="sm:flex-auto">
        <h1 class="text-base font-semibold leading-6 text-gray-900">
          Mock Interviews
        </h1>
      </div>
      <div class="mt-4 sm:ml-16 sm:mt-0 sm:flex-none">
        <button
          type="button"
          @click="openAddMockModal()"
          class="mt-2 block rounded-md bg-indigo-600 px-3 py-2 text-center text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
        >
          + Prepare Mock Interview
        </button>
      </div>
    </div>
    <!-- Add MockInterview Form Ends Here -->
    <!-- MockInterview Table Starts Here -->
    <div v-if="getInterviews.length>0" class="mt-8 flow-root">
      <div class="-mx-4 -my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
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
                  Type
                </th>
                <th
                  scope="col"
                  class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900"
                >
                  Maximum Time Allowed
                </th>
                <th
                  scope="col"
                  class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900"
                >
                  Description
                </th>
                <th
                  scope="col"
                  class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900"
                >
                  Status
                </th>
              </tr>
            </thead>
            <tbody class="divide-y divide-gray-200">
              <tr
                v-for="interview in getInterviews"
                :key="interview.name"
                @click="openViewProfile(interview)"
              >
                <td
                  class="whitespace-nowrap py-4 pl-4 pr-3 text-sm font-medium text-gray-900 sm:pl-0"
                >
                  {{ interview.name }}
                </td>
                <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                  {{ interview.type }}
                </td>
                <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                  {{ interview.max_time_allowed }}
                </td>
                <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                  {{ interview.description }}
                </td>
                <td
                  class="whitespace-nowrap px-3 py-4 text-sm text-gray-500 truncate"
                >
                  {{ interview.status }}
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
    <!-- MockInterview Table Ends Here -->

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
      <h3 class="mt-2 text-sm font-semibold text-gray-900">No mocks</h3>
      <p class="mt-1 text-sm text-gray-500">
        Get started by creating a new mock-interview.
      </p>
      <div class="mt-6">
        <button
          type="button"
          @click="openAddMockModal()"
          class="inline-flex items-center rounded-md bg-indigo-600 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
        >
          <PlusIcon class="-ml-0.5 mr-1.5 h-5 w-5" aria-hidden="true" />
          New MockInterview
        </button>
      </div>
    </div>
  </div>
  </div>
</template>

<script setup lang="ts">
import { defineProps } from "vue";

// Define Props
const props = defineProps({
  getInterviews: Array,
});

// Define Emits
const emit = defineEmits(["openModal", "openViewModal"]);

// Opens when we click 'Prepare Mock Interview' Button
const openAddMockModal = () => {
  emit("openModal", true);
};

//To View interview Data
const openViewProfile = (data: object) => {
  emit("openViewModal", data);
};
</script>

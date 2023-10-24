<template>
  <div class="px-4 sm:px-6 lg:px-8 border mt-5 ml-5 mr-7">
    <div class="sm:flex sm:items-center">
      <div class="sm:flex-auto">
        <h1 class="text-base font-semibold leading-6 text-gray-900">
          Floorplans
        </h1>
      </div>
      <div class="mt-4 sm:ml-16 sm:mt-0 sm:flex-none">
        <button
          type="button"
          @click="openAddSidebar"
          class="mt-2 block rounded-md bg-indigo-600 px-3 py-2 text-center text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
        >
          + Add Floorplan
        </button>
      </div>
    </div>
    <!-- Table format starts here and this appears only if projects are present -->
    <div
      v-if="floorPlansData.length > 0"
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
                  Build Up Area
                </th>
                <th
                  scope="col"
                  class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900"
                >
                  BedRooms
                </th>
                <th
                  scope="col"
                  class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900"
                >
                  Bathrooms
                </th>
              </tr>
            </thead>
            <tbody class="divide-y divide-gray-200">
              <tr v-for="floorPlan in floorPlansData" :key="floorPlan.name">
                <td
                  class="whitespace-nowrap py-4 pl-4 pr-3 text-sm font-medium text-gray-900 sm:pl-0"
                >
                  {{ floorPlan.name }}
                </td>
                <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                  {{ floorPlan.build_up_area }}
                </td>
                <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                  {{ floorPlan.bedrooms }}
                </td>
                <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                  {{ floorPlan.bathrooms }}
                </td>

                <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                  <div class="flex justify-center">
                    <div>
                      <PencilSquareIcon
                        class="h-5 w-5"
                        @click="openEditSidebar(floorPlan)"
                      />
                    </div>
                    <div>
                      <TrashIcon
                        class="h-5 w-5"
                        @click="deleteProject(floorPlan)"
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
        <h3 class="mt-2 text-sm font-semibold text-gray-900">No Floorplans</h3>
        <p class="mt-1 text-sm text-gray-500">
          Get started by creating a new Floorplan.
        </p>
        <div class="mt-6">
          <button
            type="button"
            @click="openAddSidebar"
            class="inline-flex items-center rounded-md bg-indigo-600 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
          >
            <PlusIcon class="-ml-0.5 mr-1.5 h-5 w-5" aria-hidden="true" />
            New Floorplans
          </button>
        </div>
      </div>
    </div>
  </div>
  <!-- Empty State Ends here -->
</template>
<script lang="ts" setup>
import { ref } from "vue";
import { PencilSquareIcon, TrashIcon } from "@heroicons/vue/24/outline";

const props = defineProps({ floorPlansData: Array });

const emit = defineEmits(["openAddSidebar", "openEditSidebar", "delete"]);
const openAddSidebar = () => {
  emit("openAddSidebar");
};

const openEditSidebar = (data: any) => {
  emit("openEditSidebar", data);
};

const deleteProject = (data: any) => {
  emit("delete", data);
};
</script>

<template>
  <div class="border ml-2 mr-3">
    <div class="sm:flex sm:items-center">
      <div class="sm:flex-auto ml-2">
        <h1 class="text-base font-semibold leading-6 text-gray-900">
          Builders
        </h1>
      </div>
      <div class="mt-4 mb-2 mr-2 sm:ml-16 sm:mt-0 sm:flex-none">
        <button
          type="button"
          @click="openAddModal()"
          class="mt-2 block rounded-md bg-indigo-600 px-3 py-2 text-center text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
        >
          + Add Builder
        </button>
      </div>
    </div>
    <ul
      role="list"
      class="grid grid-cols-1 gap-6 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 border"
    >
      <li
        v-for="builder in builderList"
        :key="builder.email"
        class="mt-2 mb-2 ml-2 col-span-1 flex flex-col divide-y divide-gray-200 rounded-lg bg-white text-center shadow"
      >
        <div class="flex flex-1 flex-col p-8">
          <PencilSquareIcon
            class="h-6 w-6 ml-[18.25rem]"
            @click="editBuilderData(builder)"
          />
          <TrashIcon
            class="h-6 w-6 ml-[20.25rem] mt-[-1.5rem]"
            @click="deleteBuilder(builder)"
          />
          <img
            class="mx-auto h-32 w-32 flex-shrink-0 rounded-full"
            :src="builder.logo"
            alt=""
          />
          <h3 class="mt-6 text-sm font-medium text-gray-900">
            {{ builder.name }}
          </h3>
          <dl class="mt-1 flex flex-grow flex-col justify-between">
            <dd class="text-sm text-gray-500">{{ builder.email }}</dd>
          </dl>
        </div>
        <div>
          <div class="-mt-px flex divide-x divide-gray-200">
            <div class="-ml-px flex w-0 flex-1">
              <a
                :href="`tel:${builder.phone_number}`"
                class="relative inline-flex w-0 flex-1 items-center justify-center gap-x-3 rounded-br-lg border border-transparent py-4 text-sm font-semibold text-gray-900"
              >
                <PhoneIcon class="h-5 w-5 text-gray-400" aria-hidden="true" />
                {{ builder.phone_number }}
              </a>
            </div>
          </div>
        </div>
      </li>
    </ul>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";
import {
  EnvelopeIcon,
  PhoneIcon,
  PencilSquareIcon,
  TrashIcon,
} from "@heroicons/vue/20/solid";

// Define Props
const props = defineProps({ builderList: Array });

// Define Emits
const emit = defineEmits(["openModal", "editModal", "deleteBuilder"]);

// Open Add Builder Modal
const openAddModal = () => {
  emit("openModal", true);
};

// Open Edit Builder Modal
const editBuilderData = (data: any) => {
  emit("editModal", data);
};

// Delete Modal
const deleteBuilder = (data: any) => {
  emit("deleteBuilder", data);
};
</script>

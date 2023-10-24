<template>
  <TransitionRoot as="template" :show="openAddProjectSidebar">
    <Dialog
      as="div"
      class="relative z-10"
      @close="openAddProjectSidebar = false"
    >
      <div class="fixed inset-0 overflow-hidden">
        <div class="absolute inset-0 overflow-hidden">
          <div
            class="pointer-events-none fixed inset-y-0 right-0 flex max-w-full pl-10"
          >
            <TransitionChild
              as="template"
              enter="transform transition ease-in-out duration-500 sm:duration-700"
              enter-from="translate-x-full"
              enter-to="translate-x-0"
              leave="transform transition ease-in-out duration-500 sm:duration-700"
              leave-from="translate-x-0"
              leave-to="translate-x-full"
            >
              <DialogPanel class="pointer-events-auto w-screen max-w-md">
                <div
                  class="flex h-full flex-col overflow-y-scroll bg-white py-6 shadow-xl"
                >
                  <div class="px-4 sm:px-6">
                    <div class="flex items-start justify-between">
                      <DialogTitle
                        class="text-base font-semibold leading-6 text-gray-900"
                        >Add Project Details</DialogTitle
                      >
                      <div class="ml-3 flex h-7 items-center">
                        <button
                          type="button"
                          class="rounded-md bg-white text-gray-400 hover:text-gray-500 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2"
                          @click="openAddProjectSidebar = false"
                        >
                          <span class="sr-only">Close panel</span>
                          <XMarkIcon class="h-6 w-6" aria-hidden="true" />
                        </button>
                      </div>
                    </div>
                  </div>
                  <form @submit.prevent="saveFormData" @reset.prevent="cancel">
                    <div
                      class="relative mt-6 flex-1 px-4 sm:px-6 border ml-2 mr-2"
                    >
                      <div class="mt-2">
                        <label
                          for="name"
                          class="block text-sm font-medium leading-6 text-gray-900"
                          >Name</label
                        >
                        <div class="mt-2">
                          <input
                            id="name"
                            v-model="form.name"
                            class="pl-2 block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                            placeholder="Enter Name"
                          />
                        </div>
                      </div>
                      <div class="mt-2">
                        <div class="mt-2">
                          <label
                            for="category"
                            class="block text-sm font-medium leading-6 text-gray-900"
                            >Category</label
                          >
                          <select
                            name="category"
                            id="category"
                            v-model="form.category"
                            class="pl-2 block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                          >
                            <option value="Residential">Residential</option>
                            <option value="Commercial">Commercial</option>
                          </select>
                        </div>
                      </div>

                      <div class="mt-2">
                        <label
                          for="sub_category"
                          class="block text-sm font-medium leading-6 text-gray-900"
                        >
                          Sub Category</label
                        >
                        <select
                          name="sub_category"
                          id="sub_category"
                          v-model="form.sub_category"
                          class="pl-2 block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                        >
                          <option value="Apartment">Apartment</option>
                          <option value="Villa">Villa</option>
                          <option value="Shop">Shop</option>
                          <option value="Plot">Plot</option>
                        </select>
                      </div>

                      <div class="mt-2">
                        <label
                          for="status"
                          class="block text-sm font-medium leading-6 text-gray-900"
                        >
                          Status</label
                        >
                        <select
                          name="status"
                          id="status"
                          v-model="form.status"
                          class="pl-2 block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                        >
                          <option value="New Venture">New Venture</option>
                          <option value="Fully Constructed">
                            Fully Constructed
                          </option>
                        </select>
                      </div>

                      <div class="mt-2">
                        <label
                          for="metric"
                          class="block text-sm font-medium leading-6 text-gray-900"
                        >
                          Metric</label
                        >
                        <select
                          name="metric"
                          id="metric"
                          v-model="form.metric"
                          class="pl-2 block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                        >
                          <option value="sq.ft">sq.ft</option>
                          <option value="sq.m">sq.m</option>
                          <option value="bigha">bigha</option>
                          <option value="centsd">cents</option>
                        </select>
                      </div>
                      <div class="mt-2">
                        <label
                          for="details"
                          class="block text-sm font-medium leading-6 text-gray-900"
                          >Details</label
                        >
                        <div class="mt-2">
                          <input
                            id="details"
                            v-model="form.details"
                            class="pl-2 block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                            placeholder="Enter Details"
                          />
                        </div>
                      </div>
                      <div class="mt-2">
                        <label
                          for="total_project_area"
                          class="block text-sm font-medium leading-6 text-gray-900"
                          >Total Project Area</label
                        >
                        <div class="mt-2">
                          <input
                            id="total_project_area"
                            v-model="form.total_project_area"
                            class="pl-2 block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                            placeholder="Enter Total Project Area"
                          />
                        </div>
                      </div>
                      <div class="mt-2">
                        <label
                          for="listing_type_name"
                          class="block text-sm font-medium leading-6 text-gray-900"
                          >Listing Type Name</label
                        >
                        <div class="mt-2">
                          <input
                            id="listing_type_name"
                            v-model="form.listing_type_name"
                            class="pl-2 block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                            placeholder="Enter Listing Type Name"
                          />
                        </div>
                      </div>

                      <div class="mt-2">
                        <div class="mt-2 mb-2 ml-[15.25rem] flex">
                          <div>
                            <button
                              type="reset"
                              class="mr-1 rounded bg-white px-2 py-1 text-sm font-semibold text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 hover:bg-gray-50"
                            >
                              Cancel
                            </button>
                          </div>
                          <div>
                            <button
                              type="submit"
                              class="rounded bg-indigo-600 px-2 py-1 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
                            >
                              Save
                            </button>
                          </div>
                        </div>
                      </div>
                    </div>
                  </form>
                </div>
              </DialogPanel>
            </TransitionChild>
          </div>
        </div>
      </div>
    </Dialog>
  </TransitionRoot>
</template>
<script setup lang="ts">
import { ref } from "vue";
import {
  Dialog,
  DialogPanel,
  DialogTitle,
  TransitionChild,
  TransitionRoot,
} from "@headlessui/vue";
import { XMarkIcon } from "@heroicons/vue/24/outline";

const form: any = ref({});

// Define Props
const props = defineProps({
  openAddProjectSidebar: Boolean,
});

// Define Emits
const emit = defineEmits(["formData", "cancel"]);

// On clicking on save button we emit form data to parent file
const saveFormData = () => {
  emit("formData", form.value);
  form.value = {};
};
// On clicking on cancel button we will close Sidebar
const cancel = () => {
  emit("cancel");
};
</script>

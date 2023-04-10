<template>
    <TransitionRoot as="template" :show="addSidebar">
      <Dialog
        as="div"
        class="relative z-10"
        @close="addSidebar = false"
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
                            @click="addSidebar = false"
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
                        <label
                          for="build_up_area"
                          class="block text-sm font-medium leading-6 text-gray-900"
                          >Build Up Area</label
                        >
                        <div class="mt-2">
                          <input
                            id="build_up_area"
                            type="number"
                            v-model="form.build_up_area"
                            class="pl-2 block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                            placeholder="Enter Build Up Area"
                          />
                        </div>
                      </div>
                      <div class="mt-2">
                        <label
                          for="bedrooms"
                          class="block text-sm font-medium leading-6 text-gray-900"
                          >Bedrooms</label
                        >
                        <div class="mt-2">
                          <input
                            id="bedrooms"
                            type="number"
                            v-model="form.bedrooms"
                            class="pl-2 block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                            placeholder="Enter Bedrooms"
                          />
                        </div>
                      </div>
                      <div class="mt-2">
                        <label
                          for="bathrooms"
                          class="block text-sm font-medium leading-6 text-gray-900"
                          >Bathrooms</label
                        >
                        <div class="mt-2">
                          <input
                            id="bathrooms"
                            type="number"
                            v-model="form.bathrooms"
                            class="pl-2 block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                            placeholder="Enter Bathrooms"
                          />
                        </div>
                      </div>
                      <div class="mt-2">
                        <label
                          for="project_id"
                          class="block text-sm font-medium leading-6 text-gray-900"
                          > Project ID</label
                        >
                        <div class="mt-2">
                          <input
                            id="project_id"
                            type="number"
                            v-model="form.project_id"
                            class="pl-2 block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                            placeholder="Enter Project ID"
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

  const form:any = ref({});
  const props =defineProps({addSidebar:Boolean});
  const emit=defineEmits(['formData']);

  const saveFormData=() =>{
    emit('formData',form.value);
    form.value={}
  }
  </script>
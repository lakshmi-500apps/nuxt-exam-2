<template>
  <TransitionRoot as="template" :show="openBuilderModal">
    <Dialog as="div" class="relative z-10" @close="openBuilderModal = false">
      <TransitionChild
        as="template"
        enter="ease-out duration-300"
        enter-from="opacity-0"
        enter-to="opacity-100"
        leave="ease-in duration-200"
        leave-from="opacity-100"
        leave-to="opacity-0"
      >
        <div
          class="fixed inset-0 bg-gray-500 bg-opacity-75 transition-opacity"
        />
      </TransitionChild>
      <div class="fixed inset-0 z-10 overflow-y-auto">
        <div
          class="flex min-h-full items-end justify-center p-4 text-center sm:items-center sm:p-0"
        >
          <TransitionChild
            as="template"
            enter="ease-out duration-300"
            enter-from="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95"
            enter-to="opacity-100 translate-y-0 sm:scale-100"
            leave="ease-in duration-200"
            leave-from="opacity-100 translate-y-0 sm:scale-100"
            leave-to="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95"
          >
            <DialogPanel
              class="relative transform overflow-hidden rounded-lg bg-white px-4 pb-4 pt-5 text-left shadow-xl transition-all sm:my-8 sm:w-full sm:max-w-lg sm:p-6"
            >
              <div>
                <div class="mt-3 text-center sm:mt-5">
                  <DialogTitle
                    as="h3"
                    class="text-base font-semibold leading-6 text-gray-900"
                    >Add Builder</DialogTitle
                  >
                  <div class="mt-2 border">
                    <form>
                      <div class="mt-2 pl-2">
                        <label
                          for="name"
                          class="block text-sm font-medium leading-6 text-gray-900 mr-[31.75rem]"
                          >Name:
                        </label>
                        <div class="mt-2">
                          <input
                            id="name"
                            v-model="form.name"
                            class="pl-2 block rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                            placeholder="Enter Name"
                          />
                        </div>
                      </div>
                      <div class="mt-2 pl-2">
                        <label
                          for="email"
                          class="block text-sm font-medium leading-6 text-gray-900 mr-[25.75rem]"
                        >
                          Email:
                        </label>
                        <div class="mt-2">
                          <input
                            type="email"
                            id="email"
                            v-model="form.email"
                            class="pl-2 block rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                            placeholder="Enter Email"
                          />
                        </div>
                      </div>
                      <div class="mt-2 pl-2">
                        <label
                          for="phone"
                          class="block text-sm font-medium leading-6 text-gray-900 mr-[31.75rem]"
                          >Phone:
                        </label>
                        <div class="mt-2">
                          <input
                            type="number"
                            id="phone"
                            v-model="form.phone_number"
                            class="pl-2 block rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                            placeholder="Enter Phone"
                          />
                        </div>
                      </div>
                      <div class="mt-2 pl-2">
                        <label
                          for="logo"
                          class="block text-sm font-medium leading-6 text-gray-900 mr-[31.75rem]"
                          >Logo:
                        </label>
                        <div class="mt-2 pb-2">
                          <input
                            id="logo"
                            type="link"
                            v-model="form.logo"
                            class="pl-2 block rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                            placeholder="Enter Logo"
                          />
                        </div>
                      </div>
                    </form>
                  </div>
                </div>
              </div>
              <div
                class="mt-5 sm:mt-6 sm:grid sm:grid-flow-row-dense sm:grid-cols-2 sm:gap-3"
              >
                <button
                  type="button"
                  class="inline-flex w-full justify-center rounded-md bg-indigo-600 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600 sm:col-start-2"
                  @click="addBuilder"
                >
                  Add Builder
                </button>
                <button
                  type="button"
                  class="mt-3 inline-flex w-full justify-center rounded-md bg-white px-3 py-2 text-sm font-semibold text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 hover:bg-gray-50 sm:col-start-1 sm:mt-0"
                  @click="openBuilderModal = false"
                  ref="cancelButtonRef"
                >
                  Cancel
                </button>
              </div>
            </DialogPanel>
          </TransitionChild>
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
import { CheckIcon, BookOpenIcon } from "@heroicons/vue/24/outline";

const form: any = ref({});

// Define Props
const props = defineProps({
  openBuilderModal: Boolean,
});

// Define Emits
const emit = defineEmits(["addBuilderData"]);

// Open Add Builder Modal
const addBuilder = () => {
  emit("addBuilderData", form.value);
  form.value = {};
};
</script>

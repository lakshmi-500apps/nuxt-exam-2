<template>
  <TransitionRoot as="template" :show="openModal">
    <Dialog as="div" class="relative z-10" @close="openModal = false">
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
                <div
                  class="mx-auto flex h-12 w-12 items-center justify-center rounded-full bg-green-100"
                >
                  <BookOpenIcon
                    class="h-6 w-6 text-green-600"
                    aria-hidden="true"
                  />
                </div>
                <div class="mt-3 text-center sm:mt-5">
                  <DialogTitle
                    as="h3"
                    class="text-base font-semibold leading-6 text-gray-900"
                    >Prepare Mock Interview</DialogTitle
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
                      <div class="mt-[-2.75rem] mr-[-15.75rem]">
                        <p
                          class="text-base font-semibold leading-6 text-gray-900"
                        >
                          Type:
                        </p>
                        <input
                          type="radio"
                          id="practice"
                          name="type"
                          value="practice"
                          v-model="form.type"
                        />
                        <label for="practice">Practice</label><br />

                        <input
                          type="radio"
                          id="videoprofile"
                          name="type"
                          value="videoprofile"
                          class="text-gray"
                          v-model="form.type"
                        />
                        <label for="videoprofile">Video Profile</label><br />
                      </div>
                      <div class="mt-2 pl-2">
                        <label
                          for="max_time_allowed"
                          class="block text-sm font-medium leading-6 text-gray-900 mr-[19.75rem]"
                        >
                          Max Time Allowed:
                        </label>
                        <div class="mt-2">
                          <input
                            type="number"
                            id="max_time_allowed"
                            v-model="form.max_time_allowed"
                            class="pl-2 block rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                            placeholder="Enter Max Time Allowed"
                          />
                        </div>
                      </div>
                      <div class="mt-2 pl-2">
                        <label
                          for="description"
                          class="block text-sm font-medium leading-6 text-gray-900 mr-[31.75rem]"
                          >Description:
                        </label>
                        <div class="mt-2">
                          <textarea
                            id="description"
                            v-model="form.description"
                            class="pl-2 block rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                            placeholder="Enter Description"
                          />
                        </div>
                      </div>
                      <div class="mt-2 pl-2">
                        <label
                          for="status"
                          class="block text-sm font-medium leading-6 text-gray-900 mr-[31.75rem]"
                          >Status:
                        </label>
                        <div class="mt-2 pb-2">
                          <input
                            id="status"
                            type="number"
                            v-model="form.status"
                            class="pl-2 block rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                            placeholder="Enter Status"
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
                  @click="addMock()"
                >
                  Add Mock
                </button>
                <button
                  type="button"
                  class="mt-3 inline-flex w-full justify-center rounded-md bg-white px-3 py-2 text-sm font-semibold text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 hover:bg-gray-50 sm:col-start-1 sm:mt-0"
                  @click="openModal = false"
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
  openModal: Boolean,
});

// Define Emits
const emit = defineEmits(["addMock"]);

// Data after collecting from user we will send it to Parent file
const addMock = () => {
  emit("addMock", form.value);
  form.value = {};
};
</script>

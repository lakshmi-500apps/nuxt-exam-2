<template>
    <!-- View Question Bank Starts Here -->
    <TransitionRoot as="template" :show="openViewSidebar">
      <Dialog as="div" class="relative z-10" @close="openViewSidebar = false">
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
                          >View Question Bank</DialogTitle
                        >
                        <div class="ml-3 flex h-7 items-center">
                          <button
                            type="button"
                            class="rounded-md bg-white text-gray-400 hover:text-gray-500 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2"
                            @click="openViewSidebar = false"
                          >
                            <span class="sr-only">Close panel</span>
                            <XMarkIcon class="h-6 w-6" aria-hidden="true" />
                          </button>
                        </div>
                      </div>
                    </div>
                    <!-- Data is prefilled in input fields -->
                    <form  @reset.prevent="cancel">
                      <div
                        class="relative mt-6 flex-1 px-4 sm:px-6 border ml-2 mr-2"
                      >
                        <div class="mt-2">
                          <label
                            for="category"
                            class="block text-sm font-medium leading-6 text-gray-900"
                            >Category</label
                          >
                          <div class="mt-2">
                            <input
                              id="category"
                              v-model="questionBankData.category"
                              class="pl-2 block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                              placeholder="Enter Category"
                            />
                          </div>
                        </div>
                        <div class="mt-2">
                          <label
                            for="skill"
                            class="block text-sm font-medium leading-6 text-gray-900"
                            >Skill</label
                          >
                          <div class="mt-2">
                            <input
                              id="skill"
                              v-model="questionBankData.skill"
                              class="pl-2 block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                              placeholder="Enter Skill"
                            />
                          </div>
                        </div>
  
                        <div class="mt-2">
                          <label
                            for="question"
                            class="block text-sm font-medium leading-6 text-gray-900"
                            >Question</label
                          >
                          <div class="mt-2">
                            <input
                              id="question"
                              v-model="questionBankData.question"
                              class="pl-2 block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                              placeholder="Enter Question"
                            />
                          </div>
                        </div>
  
                        <div class="mt-2">
                          <label
                            for="answer"
                            class="block text-sm font-medium leading-6 text-gray-900"
                            >Answer
                          </label>
                          <div class="mt-2">
                            <input
                              id="answer"
                              v-model="questionBankData.answer"
                              class="pl-2 block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                              placeholder="Enter Answer "
                            />
                          </div>
                        </div>
  
                        <div class="mt-2">
                          <label
                            for="sub_skill"
                            class="block text-sm font-medium leading-6 text-gray-900"
                            >Sub Skill</label
                          >
                          <div class="mt-2">
                            <input
                              id="sub_skill"
                              v-model="questionBankData.sub_skill"
                              class="pl-2 block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                              placeholder="Enter Sub Skill"
                            />
                          </div>
                        </div>
                        <div class="mt-2">
                          <label
                            for="question_url"
                            class="block text-sm font-medium leading-6 text-gray-900"
                            >Question URL</label
                          >
                          <div class="mt-2">
                            <input
                              id="question_url"
                              v-model="questionBankData.question_url"
                              class="pl-2 block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                              placeholder="Enter Question URL"
                            />
                          </div>
                        </div>
                        <div class="mt-2">
                          <label
                            for="answer_hint"
                            class="block text-sm font-medium leading-6 text-gray-900"
                            >Answer Hint</label
                          >
                          <div class="mt-2">
                            <input
                              id="answer_hint"
                              v-model="questionBankData.answer_hint"
                              class="pl-2 block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                              placeholder="Enter Answer Hint"
                            />
                          </div>
                        </div>
                        <div class="mt-2">
                          <label
                            for="explanation"
                            class="block text-sm font-medium leading-6 text-gray-900"
                            >Explanation</label
                          >
                          <div class="mt-2">
                            <input
                              id="explanation"
                              v-model="questionBankData.explanation"
                              class="pl-2 block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                              placeholder="Enter Explanation"
                            />
                          </div>
                        </div>
  
                        <div class="mt-2">
                          <label
                            for="marks"
                            class="block text-sm font-medium leading-6 text-gray-900"
                            >Marks</label
                          >
                          <div class="mt-2">
                            <input
                              id="marks"
                              type="number"
                              v-model="questionBankData.marks"
                              class="pl-2 block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                              placeholder="Enter Marks"
                            />
                          </div>
                        </div>
  
                        <div class="mt-2">
                          <div class="mt-2 mb-2 ml-[18.25rem] flex">
                            <div>
                              <button
                                type="reset"
                                class="mr-1 rounded bg-white px-2 py-1 text-sm font-semibold text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 hover:bg-gray-50"
                              >
                                Cancel
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
    <!-- View Question Bank Ends Here -->
  </template>
  <script setup lang="ts">
  import { ref, defineProps, defineEmits } from "vue";
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
    openViewSidebar: Boolean,
    questionBankData:Object
  });
  
  // Define Emits
  const emit = defineEmits(["cancel"]);
  
  // On clicking on cancel button we will close Sidebar
  const cancel = () => {
    emit("cancel");
  };
  </script>
  
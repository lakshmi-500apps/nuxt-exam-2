<template>
  <div class="px-4 sm:px-6 lg:px-8 border mt-5 ml-5 mr-7">
    <div class="sm:flex sm:items-center">
      <div class="sm:flex-auto">
        <h1 class="text-base font-semibold leading-6 text-gray-900">
          List Of people
        </h1>
      </div>
      <div class="mt-4 sm:ml-16 sm:mt-0 sm:flex-none">
        <button
          type="button"
          @click="openAddModal"
          class="mt-2 mb-2 block rounded-md bg-indigo-600 px-3 py-2 text-center text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
        >
          + Add Details
        </button>
      </div>
    </div>
    <div class="mt-2">
      <input
        type="text"
        name="text"
        id="text"
        v-model="searchValue"
        class="block mb-2 pl-2 rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
        placeholder="Search"
      />
    </div>
    <ul
      role="list"
      class="border grid grid-cols-1 gap-6 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4"
    >
      <li
        v-for="(person,index) in people"
        :key="person.name"
        class="col-span-1 flex flex-col divide-y divide-gray-200 rounded-lg bg-white text-center shadow"
      >
        <div class="flex flex-1 flex-col p-8">
          <div class="flex flex-1 flex-col p-8">
            <PencilSquareIcon
              class="h-6 w-6 ml-[14.25rem]"
              @click="editDetails(person,index)"
            />
            <TrashIcon @click="(open=true),(deleteIndex =index)" class="h-6 w-6 ml-[16.25rem] mt-[-1.5rem]" />
          </div>
          <div class="flex justify-center">
            <div>
              <h3 class="mt-6 text-sm font-medium text-gray-900">
                {{ person.name }}
              </h3>
            </div>
            <div>
              <dd class="mt-5 ml-2">
                <span
                  class="rounded-full bg-green-100 px-2 py-1 text-xs font-medium text-green-800"
                  >{{ person.gender }}</span
                >
              </dd>
            </div>
          </div>
          <dl class="mt-1 flex flex-grow flex-col justify-between">
            <dd class="text-sm text-gray-500">{{ person.age }}</dd>

            <dd class="text-sm text-gray-500">{{ person.DOB }}</dd>
          </dl>
        </div>
        <div></div>
      </li>
    </ul>
    <Bar :data="data" :options="options" />
    <TransitionRoot as="template" :show="open">
    <Dialog as="div" class="relative z-10" @close="open = false">
      <TransitionChild as="template" enter="ease-out duration-300" enter-from="opacity-0" enter-to="opacity-100" leave="ease-in duration-200" leave-from="opacity-100" leave-to="opacity-0">
        <div class="fixed inset-0 bg-gray-500 bg-opacity-75 transition-opacity" />
      </TransitionChild>

      <div class="fixed inset-0 z-10 overflow-y-auto">
        <div class="flex min-h-full items-end justify-center p-4 text-center sm:items-center sm:p-0">
          <TransitionChild as="template" enter="ease-out duration-300" enter-from="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95" enter-to="opacity-100 translate-y-0 sm:scale-100" leave="ease-in duration-200" leave-from="opacity-100 translate-y-0 sm:scale-100" leave-to="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95">
            <DialogPanel class="relative transform overflow-hidden rounded-lg bg-white px-4 pb-4 pt-5 text-left shadow-xl transition-all sm:my-8 sm:w-full sm:max-w-lg sm:p-6">
              <div>
                <div class="mt-3 text-center sm:mt-5">
                  <DialogTitle as="h3" class="text-base font-semibold leading-6 text-gray-900">Delete Confirmation</DialogTitle>
                </div>
              </div>
              <div class="mt-5 sm:mt-6 sm:grid sm:grid-flow-row-dense sm:grid-cols-2 sm:gap-3">
                <button type="button" class="inline-flex w-full justify-center rounded-md bg-indigo-600 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600 sm:col-start-2" @click=" deleteDetails(deleteIndex)">Delete</button>
                <button type="button" class="mt-3 inline-flex w-full justify-center rounded-md bg-white px-3 py-2 text-sm font-semibold text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 hover:bg-gray-50 sm:col-start-1 sm:mt-0" @click="open = false" ref="cancelButtonRef">Cancel</button>
              </div>
            </DialogPanel>
          </TransitionChild>
        </div>
      </div>
    </Dialog>
  </TransitionRoot>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";
import { EnvelopeIcon, PhoneIcon } from "@heroicons/vue/20/solid";
import { PencilSquareIcon, TrashIcon } from "@heroicons/vue/24/outline";
import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  BarElement,
  CategoryScale,
  LinearScale
} from 'chart.js'
import { Bar } from 'vue-chartjs'
import { Dialog, DialogPanel, DialogTitle, TransitionChild, TransitionRoot } from '@headlessui/vue'

const open = ref(false)

ChartJS.register(CategoryScale, LinearScale, BarElement, Title, Tooltip, Legend)

const searchValue = ref("");
const dataValue = ref({});
const deleteIndex=ref(0);
const emit = defineEmits(["openAddModal", "editDetails","deleteDetails"]);
const props = defineProps({ people: Array });
let nameLetters=props.people.map(person => person.name.substring(0,1).toUpperCase());
nameLetters.forEach((letter) => {if(dataValue.value[letter]) dataValue.value[letter]++;         else dataValue.value[letter] =1;})

const data= {
        labels:Object.keys(dataValue.value),
        datasets: [{ data: Object.values(dataValue.value) }]
      }

const  options= {
        responsive: true
      }

const openAddModal = () => {
  emit("openAddModal");
};

const editDetails = (data: any,index:any) => {
  emit("editDetails", data,index);
};

const deleteDetails=(data:any) =>{
    emit('deleteDetails',data);
    open.value = false
}
</script>

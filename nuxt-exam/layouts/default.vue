<template>
   <nav class="container mx-auto p-4 ">
              <div class="flex justify-evenly">
                <div><NuxtLink to="/testcollection" class="font-bold"><div class="flex ml-2"><div><ClipboardDocumentIcon class="h-6 w-6 mr-2"/></div><div>Bank</div></div></NuxtLink></div>
              <div><NuxtLink to="/project" class="font-bold"><div class="flex ml-2"><div><BuildingOfficeIcon class="h-6 w-6 mr-2"/></div><div>Project</div></div></NuxtLink></div>
              <div><NuxtLink to="/mockinterview" class="font-bold"><div class="flex ml-2"><div><IdentificationIcon class="h-6 w-6 mr-2"/></div><div>Mock Interviews</div></div></NuxtLink></div>
            </div></nav>
          <div>
            <slot />
          </div>
</template>
<script setup lang="ts">
import {ClipboardDocumentIcon,BuildingOfficeIcon,IdentificationIcon} from '@heroicons/vue/24/outline'
</script>


<template>
   <nav class="container mx-auto p-4 ">
              <div class="flex justify-evenly">
                <div><NuxtLink to="/testcollection" class="font-bold"><div class="flex ml-2"><div><ClipboardDocumentIcon class="h-6 w-6 mr-2"/></div><div>Bank</div></div></NuxtLink></div>
              <div><NuxtLink to="/project" class="font-bold"><div class="flex ml-2"><div><BuildingOfficeIcon class="h-6 w-6 mr-2"/></div><div>Project</div></div></NuxtLink></div>
              <div><NuxtLink to="/mockinterview" class="font-bold"><div class="flex ml-2"><div><IdentificationIcon class="h-6 w-6 mr-2"/></div><div>Mock Interviews</div></div></NuxtLink></div>
              <div><NuxtLink to="/builder" class="font-bold"><div class="flex ml-2"><div><HomeModernIcon class="h-6 w-6 mr-2"/></div><div>Builder</div></div></NuxtLink></div>
              <div><NuxtLink to="/floorplan" class="font-bold"><div class="flex ml-2"><div><BuildingStorefrontIcon class="h-6 w-6 mr-2"/></div><div>Floorplans</div></div></NuxtLink></div>
              <div><NuxtLink to="/test3" class="font-bold"><div class="flex ml-2"><div><ClipboardDocumentIcon class="h-6 w-6 mr-2"/></div><div>Test 3</div></div></NuxtLink></div>
            </div></nav>
          <div>
            <slot />
          </div>
</template>
<script setup lang="ts">
import {ClipboardDocumentIcon,BuildingOfficeIcon,IdentificationIcon,HomeModernIcon,BuildingStorefrontIcon} from '@heroicons/vue/24/outline'
</script>


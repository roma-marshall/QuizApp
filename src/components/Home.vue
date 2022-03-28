<template>
  <main class="flex h-screen justify-center">
    <div class="bg-white container mx-auto shadow-lg rounded-lg px-12 py-6">
      <div class="text-right text-gray-800">
        <p class="text-sm leading-3">Score</p>
        <p class="font-bold">60</p>
      </div>
      <div class="bg-white shadow-lg p-2 rounded-full w-full h-10">
        <div class="bg-blue-700 rounded-full w-11/12 h-full"></div>
      </div>
      <div class="rounded-lg bg-gray-100 p-2 morph-1 text-center font-bold text-gray-800 mt-8">
        <div class="bg-white p-5">
          Who is the most powerful...?
        </div>
      </div>
      <div class="mt-8">
        <div class="morph-1 bg-gray-100 p-2 rounded-lg mb-3 relative">
          <div class="bg-blue-700 p-1 transform rotate-45 rounded-md text-white h-10 w-10
        fond-bold absolute right-0 top-0 shadow-md">
            <p class="transform -rotate-45">+10</p>
          </div>
          <div class="bg-white rounded-lg font-bold flex p-2">
            <div class="bg-gray-400 p-3 rounded-lg">A</div>
            <div class="flex items-center pl-6">Option 1</div>
          </div>
        </div>
      </div>
      <div class="mt-8 text-center">
        <div class="h-1 w-12 bg-gray-800 rounded-full mx-auto"></div>
        <p class="text-gray-800 font-bold">2/10</p>
      </div>
    </div>
  </main>
</template>

<script>
import {ref} from 'vue'

export default {
  
}
</script>

<style scoped>
.morph-1 {
  box-shadow: 6px 6px 18px rgba(0, 0, 0, 0.09), -6px -6px 18px #ffffff;
}
</style>
<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <header>
    <nav class="flex items-center justify-between flex-wrap bg-teal-500 p-6">
      <div class="w-full block flex-grow lg:flex lg:items-center lg:w-auto">
        <div class="text-sm lg:flex-grow">
          <RouterLink class="block mt-4 lg:inline-block lg:mt-0 text-teal-200 hover:text-white mr-4" to="/offer">Send offer to chat</RouterLink>
        </div>
      </div>
    </nav>
  </header>

  <div class="md:container md:mx-auto pt-6">
    <RouterView />
  </div>
</template>

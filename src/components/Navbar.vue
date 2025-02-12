<script setup>
  import { RouterLink, useRoute } from 'vue-router';
  import logo from '@/assets/img/logo.png';

  const isActiveLink = (routePath) => {
  const route = useRoute();
  return route.path === routePath;
};

</script>

<template>
    <nav class="bg-white-900 border-b border-sky-600">
      <div class="mx-auto max-w-7xl px-2 sm:px-6 lg:px-8">
        <div class="flex h-20 items-center justify-between">
          <div
            class="flex flex-1 items-center justify-center md:items-stretch md:justify-start"
          >
            <!-- Logo -->
            <RouterLink class="flex flex-shrink-0 items-center mr-4" to="/">
              <img class="h-10 w-auto" :src="logo" alt="Stellar Blue" />
            </RouterLink>
            <div class="md:ml-auto">
              <div class="flex space-x-2">
                <RouterLink
                  to="/"
                  :class="[isActiveLink('/') ? 'text-sky-600 underline decoration-sky-600' : 'hover:text-sky-600 text-black-800 hover:underline hover:decoration-sky-600', 'rounded-md', 'px-3', 'py-2']"
                  >Home
                  </RouterLink>
                <RouterLink
                  to="/app"
                  :class="[isActiveLink('/app') ? 'text-sky-600 underline decoration-sky-600' : 'hover:text-sky-600 text-black-800 hover:underline hover:decoration-sky-600', 'rounded-md', 'px-3', 'py-2']"
                  >App
                </RouterLink>
              </div>
            </div>
          </div>
        </div>
      </div>
    </nav>
</template>
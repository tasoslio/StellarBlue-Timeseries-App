<script setup>
    import Card from './Card.vue';
    import { RouterLink } from 'vue-router';
</script>

<template>
    <section class="py-4">
      <div class="container-xl lg:container m-auto">
        <div class="grid grid-cols-1 md:grid-cols-2 gap-4 p-4 rounded-lg">
          <Card>
            <h2 class="text-2xl font-bold">Github Repository Project</h2>
            <p class="mt-2 mb-4">
              Click the button to navigate in the repository of the project.
            </p>
            <a
              href="https://github.com/tasoslio/StellarBlue-Timeseries-App"
              class="inline-block bg-black text-white rounded-lg px-4 py-2 hover:bg-gray-700"
            >
              Github
          </a>
          </Card>
          <Card bg="bg-sky-100">
            <h2 class="text-2xl font-bold">Test the Timeseries Data Visualization</h2>
            <p class="mt-2 mb-4">
              Click the button to check the Timeseries App.
            </p>
            <RouterLink
              to="/app/"
              class="inline-block bg-sky-600 text-white rounded-lg px-4 py-2 hover:bg-sky-800"
            >
              View App
            </RouterLink>
          </Card>
        </div>
      </div>
    </section>
</template>
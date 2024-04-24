<!-- DataCard.vue -->

<template>
    <div class="card">
      <fwb-card
        :img-src="info.image"
        img-alt="Show image"
        variant="image"
        class="mb-4"
      >
        <div class="p-5">
          <h5 class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white">
            {{ info.title }}
          </h5>
          <p class="font-normal text-gray-700 dark:text-gray-400">
            {{ info.description }}
          </p>
          <p class="font-normal text-gray-700 dark:text-gray-400">
            Genres: {{ info.genres }}
          </p>
          <div v-if="info.streamingInfo.length">
            <h6 class="mt-4 mb-1 text-gray-900 dark:text-white">Available on:</h6>
            <ul>
              <li v-for="stream in info.streamingInfo" :key="stream.link" class="text-gray-700 dark:text-gray-400">
                {{ stream.service || 'Unknown Service' }} ({{ stream.streamingType || 'Unknown Type' }}) - 
                <a :href="stream.link" target="_blank">Watch Now</a>
              </li>
            </ul>
          </div>
        </div>
      </fwb-card>
    </div>
  </template>
  
  <script setup>
  import { FwbCard } from 'flowbite-vue'
  </script>
  
  <script>
export default {
    mounted() {
    console.log(this.info); // Log to see the data each card receives
  },
  props: {
    info: {
      type: Object,
      required: true
    }
  },
  filters: {
    capitalize(value) {
      if (!value) return '';
      value = value.toString();
      return value.charAt(0).toUpperCase() + value.slice(1);
    }
  }
}
</script>
  
  <style scoped>
.card {
 flex: 0 1 calc(50% - 20px); /* Two cards per row on smaller screens */
  margin: 15px;
  max-width: 300px;  /* Ensures that the card does not grow beyond 300px */
  
}
  </style>
  
<template>
    <div>
      <form @submit.prevent="fetchData">
        <!-- form elements here -->
      </form>
      <div v-if="response">
        <h3>Results:</h3>
        <div v-for="item in response" :key="item.title" class="card-container">
          <DataCard :info="item" />
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import DataCard from './components/DataCard.vue';
  
  export default {
    components: {
      DataCard
    },
    // the rest of your component's code...
  }
  </script>
  
  <style>
  .card-container {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
  }
  </style>
  
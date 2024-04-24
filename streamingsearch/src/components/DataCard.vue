<template>
    <div class="card">
      <div class="card-body">
        <h5 class="card-title">{{ info.title }} ({{ info.type }})</h5>
        <p class="card-text">Year: {{ info.year }}</p>
        <p class="card-text">Genres: {{ info.genres }}</p>
        <p class="card-status">Status: {{ info.status }}</p>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      info: {
        type: Object,
        required: true
      }
    }
  }
  </script>
  
  <style scoped>
  .card {
    margin-bottom: 20px;
  }
  </style>
  
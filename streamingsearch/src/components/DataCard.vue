<template>
    <div class="card">
      <img :src="info.image" alt="Poster" class="card-img-top">
      <div class="card-body">
        <h5 class="card-title">{{ info.title }}</h5>
        <p class="card-text">{{ info.description }}</p>
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
    width: 18rem;
    margin: 1rem;
  }
  .card-img-top {
    width: 100%;
    height: auto;
  }
  </style>
  
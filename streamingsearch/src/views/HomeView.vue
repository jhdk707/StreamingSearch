<template>
  <div>
    <form @submit.prevent="fetchData">
      <input v-model="form.title" placeholder="Enter a show or movie title">
      <select v-model="form.country">
        <option value="us">USA</option>
        <option value="uk">UK</option>
        <!-- Add more countries as needed -->
      </select>
      <select v-model="form.show_type">
        <option value="all">All</option>
        <option value="movie">Movie</option>
        <option value="show">TV Show</option>
      </select>
      <button type="submit">Search</button>
    </form>

    <!-- Displaying the response data -->
    <div v-if="response">
      <h3>Results:</h3>
      <pre>{{ response }}</pre>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      form: {
        country: 'us',
        title: '',
        show_type: 'all'
      },
      response: null,
    };
  },
  methods: {
    async fetchData() {
      const options = {
        method: 'GET',
        url: 'https://streaming-availability.p.rapidapi.com/search/title',
        params: this.form,
        headers: {
          'X-RapidAPI-Key': 'YOUR_RAPIDAPI_KEY',
          'X-RapidAPI-Host': 'streaming-availability.p.rapidapi.com'
        }
      };

      try {
        const result = await axios.request(options);
        this.response = result.data;
      } catch (error) {
        console.error('Error fetching data:', error);
        this.response = null;
      }
    }
  }
}
</script>

<style>

input, option, select{
  color:black;
}

</style>
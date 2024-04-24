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
    <div v-if="response && response.length">
      <h3>Results:</h3>
      <DataCard v-for="item in response" :key="item.title" :info="item" />
    </div>
    <div v-else>No results found.</div>
  </div>
</template>

<script>
import axios from 'axios';
import DataCard from '@/components/DataCard.vue';


export default {
  components: {
    DataCard
  },
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
          'X-RapidAPI-Key': '16f87e2059mshe937410fce7f782p1d1cc9jsnae5dd54150f4',  
          'X-RapidAPI-Host': 'streaming-availability.p.rapidapi.com'
        }
      };
      try {
    const result = await axios.request(options);
    if (result.data && result.data.result) {
      this.response = result.data.result.map(item => ({
        title: item.title,
        type: item.type,
        year: item.type === 'series' ? item.firstAirYear : item.year,
        genres: item.genres.map(genre => genre.name).join(', '),
        status: item.status ? item.status.statusText : 'N/A'
      }));
    } else {
      this.response = [];
    }
      } catch (error) {
        console.error('Error fetching data:', error);
        if (error.response) {
          console.error('Response status:', error.response.status);
          console.error('Response data:', error.response.data);
        }
        this.response = null;
      }
    }
  }
}
</script>

<style>
input, select {
  color: black;
}
</style>

<!-- HomeView.vue -->

<template>
  <div>
    <form @submit.prevent="fetchData">
      <fwb-input v-model="form.title" label="Small" placeholder="Enter a show or movie title"/>
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
      <fwb-button gradient="green-blue" outline type="submit" size="lg">Search</fwb-button>
    </form>

  
    <!-- Displaying the response data -->
    <div class="grid-container">
    <div v-if="response && response.length">
      <DataCard
        v-for="item in response"
        :key="item.title"
        :info="item"
      />
    </div>
    <div v-else>
      No results found.
    </div>
  </div>
  </div>
</template>

<script setup>
import { FwbInput, FwbButton } from 'flowbite-vue'
</script>

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
        image: item.poster_path || 'default_image_url_here',
        description: `Type: ${item.type}, Year: ${item.year || item.firstAirYear}, Status: ${item.status ? item.status.statusText : 'N/A'}`,
        genres: item.genres.map(genre => genre.name).join(', '),
        streamingInfo: item.streamingInfo.us ? item.streamingInfo.us.map(service => ({
          service: service.service,
          streamingType: service.streamingType,
          quality: service.quality,
          link: service.link
        })) : []
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

select{
border-radius: 5px;
}

.grid-container {
  margin-top: 2%;
  color: white;
  max-height: 800px;
  max-width: 100vw;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-evenly;
}

.card {
  flex: 0 1 calc(50% - 20px); /* Two cards per row on smaller screens */
 margin: 15px;
}
</style>


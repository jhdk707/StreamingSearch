<script setup>
// import { RouterLink, RouterView } from 'vue-router'
import Header from './components/HeaderBar.vue'
import HomeView from './views/HomeView.vue';
</script>

<template class="overflow-y-auto">
  <div class="body">
    <div class="headercontainer">
      <Header/>
    </div>
    <div class="viewcontainer">
      <HomeView />
    </div>
  </div>
</template> 

<style>
.body, .headercontainer, .viewcontainer {
  width: 100%; 
}

.viewcontainer{
padding: 2em;
}

</style>
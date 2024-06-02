<script>
import { RouterLink, RouterView } from 'vue-router';
import Navbar from './components/Header.vue'
// import Repository from './components/Repository.vue'

export default{
  components:{
    Navbar,
    // Repository
  }
}


</script>

<template>
  <Navbar/>
  <!-- <Repository/> -->
  <RouterView />
  
</template>


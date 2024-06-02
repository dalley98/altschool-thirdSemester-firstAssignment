<script>
import GitHubIcon from './icons/GitHubIcon.vue';

export default{
  name: "Header",
  components:{
    GitHubIcon,
  }
}
</script>

<template>
  <div class="header">
    <GitHubIcon class="github-icon"/>
    <h1>Ore's GitHub.</h1>
  </div>
</template>

<style scoped>
.header{
  display: flex;
  gap: 10px;
  padding: 20px;
  align-items: center;
  text-align: center;
  justify-content: center;
}
</style>

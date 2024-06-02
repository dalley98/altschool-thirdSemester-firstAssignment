<script>
import axios from "axios";

export default {
  name: "Repository",

  data() {
    return {
      repos: [],
    };
  },

  methods: {
    fetchRepos: function () {
      axios.get("https://api.github.com/users/dalley98/repos").then((res) => {
        this.repos = this.repos.concat(res.data);
      });
    },

    nextPage: function () {
      this.currentPage++;
    },
  },

  mounted() {
    this.fetchRepos();
  },
};
</script>

<template>
  <div class="repo-container">
    <div v-for="repo in repos" :key="repo.id" class="single-repo">
      <router-link :to="`/details/${repo.name}`"
        ><h2>{{ repo.name }}</h2></router-link
      >
      <p>Language:{{ repo.language }}</p>
      <p>Start date & time:{{ repo.created_at }}</p>
      <p>Visibility:{{ repo.visibility }}</p>
    </div>
  </div>
  <!-- <div class="paginate">
    <button class="btn">Prev</button>
    <button class="btn" @click="nextPage">Next</button>
  </div> -->
</template>

<style>
.repo-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 20px;
  width: 90%;
  margin: 0 auto;
}

.repo-container a {
  text-decoration: none;
  color: #dfcece;

  &:hover {
    text-decoration: underline;
  }
}

.single-repo {
  border: 1px solid;
  border-radius: 5px;
  padding: 10px;

  &:hover {
    border: 2px solid;
  }
}

/* .paginate{
  display: flex;
  gap: 20px;
  justify-content: center;
  margin-block-start: 20px;
}

.btn{
  width: 5rem;
  font-weight: bold;
} */
</style>

<script>
import axios from "axios";
import BranchIcon from "./icons/BranchIcon.vue";
import ForkIcon from "./icons/ForkIcon.vue";
import StarIcon from "./icons/StarIcon.vue";
import WatchIcon from "./icons/WatchIcon.vue";
import BackIcon from "./icons/BackIcon.vue";

export default {
  name: "RepoDetails",

  data() {
    return {
      details: [],
      branches: [],
      deployment: [],
    };
  },

  methods: {
    fetchData: function () {
      axios
        .get(`https://api.github.com/repos/dalley98/${this.$route.params.id}`)
        .then((res) => (this.details = res.data));

      axios
        .get(
          `https://api.github.com/repos/dalley98/${this.$route.params.id}/branches`
        )
        .then((res) => (this.branches = res.data));

      axios
        .get(
          `https://api.github.com/repos/dalley98/${this.$route.params.id}/deployments`
        )
        .then((res) => (this.deployment = res.data));
    },
  },

  mounted() {
    this.fetchData();
  },

  components: {
    StarIcon,
    WatchIcon,
    ForkIcon,
    BranchIcon,
    BackIcon
  },
};
</script>

<template>
  <div id="repodetail">
    <router-link :to="`/`"><button class="back-btn"><BackIcon /></button></router-link>
    <div class="repodetail-card">
      <h2 class="repo-name">{{ details.name }}</h2>
      <div class="repo-mini-container">
        <div class="repo-mini">
          <StarIcon class="icons" />
          <p>Stars: {{ details.stargazers_count }}</p>
        </div>
        <div class="repo-mini">
          <WatchIcon class="icons" />
          <p>Watch: {{ details.watchers }}</p>
        </div>
        <div class="repo-mini">
          <ForkIcon class="icons" />
          <p>Forks: {{ details.forks }}</p>
        </div>
        <div class="repo-mini">
          <BranchIcon class="icons" />
          <p>Branches: {{ branches.length }}</p>
        </div>
      </div>
      <p v-if="details.language === null">Main Language: None</p>
      <p v-else>Main Language: {{ details.language }}</p>
      <p v-if="deployment.length === 0">Live Site: None</p>
      <p v-else>
        Live Site:
        <a :href="`${details.homepage}`"
          >dalley98.github.io/{{ details.name }}</a
        >
      </p>
      <p>
        <a :href="`https://github.com/${details.full_name}`">View on GitHub</a>
      </p>
    </div>
  </div>
</template>

<style scoped>
#repodetail {
  margin: 0 auto;
  width: 90%;
  max-width: 620px;
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.repodetail-card {
  border: 1px solid;
  border-radius: 5px;
  padding: 10px;

  &:hover{
    border: 2px solid;
  }
}

.repo-mini-container {
  display: flex;
  flex-direction: column;
  gap: 3px;
}

.repo-mini {
  display: flex;
  gap: 10px;
  align-items: center;
}

.icons {
  width: 15px;
  height: 15px;
  fill: white;
}

.repodetail-card a {
  color: white;
  text-decoration: none;

  &:hover {
    text-decoration: underline;
  }
}

.back-btn {
  padding: 5px;
  border: none;
  border-radius: 10px;
  width: 40px;

  &:hover{
    background-color: hsl(0, 0%, 80%);
  }

  &:active{
    background-color: hsl(0, 0%, 60%);
  }
}
</style>

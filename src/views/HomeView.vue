<script>
import SingleProject from '../components/projects/SingleProject.vue';
import FilterNav from '../components/FilterNav.vue';
export default {
  name: 'HomeView',
  components: {
    SingleProject,
    FilterNav,
  },

  data() {
    return {
      projects: [],
      current: 'all',

    };
  },
  mounted() {
    fetch('http://localhost:3000/projects')
      .then((response) => response.json())
      .then((data) => (this.projects = data))
      .catch((error) => console.error(error));
  },
  methods: {
    deleteProject(id) {
      this.projects = this.projects.filter((project) => project.id !== id);
    },
    completeProject(id) {
      let p = this.projects.find((project) => project.id === id);
      p.complete= !p.complete;
    },
  },
  computed: {
    filteredProjects() {
   if(this.current === 'completed') {
     return this.projects.filter((project) => project.complete);
    }
    if(this.current === 'ongoing') {
      return this.projects.filter((project) => !project.complete);
    }
    return this.projects;
  },
}
  
};
</script>

<template>
  <div>
    <FilterNav  @update-filter="current=$event" :current="current"/>
  </div>
  <div class="flex justify-center mt-5">
    <div class="grid gap-4 grid-cols-2 ">
      <div v-if="projects.length">
        <div v-for="project in filteredProjects" :key="project.id" class="fixed-width">
          <SingleProject :project="project"  @delete="deleteProject" @complete="completeProject" class=""/>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.fixed-width {
  width: 600px; /* Set your desired fixed width */
}
</style>

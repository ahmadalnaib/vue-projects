<script>
import SingleProject from '../components/projects/SingleProject.vue';
export default {
  name: 'HomeView',
  components: {
    SingleProject,
  },

  data() {
    return {
      projects: [],

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
};
</script>

<template>
  <div class="flex justify-center mt-5">
    <div class="grid gap-4 grid-cols-2 ">
      <div v-if="projects.length">
        <div v-for="project in projects" :key="project.id" class="fixed-width">
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

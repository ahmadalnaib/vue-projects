<script>
export default {
  name: 'SingleProject',
  props: ['project'],
  data() {
    return {
      showDec: false,
      uri: 'http://localhost:3000/projects/' + this.project.id,
    };
  },
  methods: {
    showDescription() {
      this.showDec = !this.showDec;
    },
    deleteProject() {
      fetch(this.uri, {
        method: 'DELETE',
      })
     .then(()=> this.$emit('delete', this.project.id))
      .catch((error) => console.error(error));
    },
    doneProject() {
  fetch(this.uri, {
    method: 'PUT',
    headers: {
      'Content-Type': 'application/json',
    },
    body: JSON.stringify({
      complete: !this.project.complete,
    })
  })
  .then(() => {
    this.$emit('complete', this.project.id);
  })
  .catch((error) => console.error(error));
}

  },
};
</script>

<template>
  <div class="bg-gray-100 shadow-sm mb-5 p-5 border-s-8 border-red-600" :class="{complete:project.complete}">
    <div class="actions">
      <h2  @click="showDescription" class="text-xl cursor-pointer">{{ project.title }}</h2>
      <div class="icons mt-4 flex justify-end">
        <div class="">
          <span class="bg-gray-300 p-2 rounded-md cursor-pointer me-1" @click="doneProject">Done</span>
          <router-link :to="{name:'editProject',params:{id:project.id}}" class="bg-gray-300 p-2 rounded-md cursor-pointer me-1">
            <span>Edit</span>
          </router-link>
          <span class="bg-gray-300 p-2 rounded-md cursor-pointer" @click="deleteProject">Delete</span>

        </div>

      </div>
    </div>
    <div v-if="showDec" class=" mt-4">
      <p>{{ project.description }}</p>
    </div>
  </div>
</template>


<style scoped>

.complete{
  background-color: #f0f0f0;
  border-left: 4px solid green;
}


</style>
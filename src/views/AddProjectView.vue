<script>
export default {
  data() {
    return {
      title: '',
      description: ''
    }
  },
  methods: {
    handleSubmit() {
      // Handle form submission
      let project = {
        title: this.title,
        description: this.description,
        complete: false
      }
      fetch('http://localhost:3000/projects', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify(project)
      })
      .then(() => {
        this.$router.push({ name: 'home' })
      })

    }
  }
}
</script>

<template>
  <div class="max-w-md mx-auto mt-10">
    <h1 class="text-2xl font-bold mb-6">Add Project</h1>
    <form @submit.prevent="handleSubmit">
      <div class="mb-4">
        <label for="title" class="block text-sm font-medium text-gray-700">Title</label>
        <input type="text" id="title" v-model="title" class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm">
      </div>
      <div class="mb-4">
        <label for="description" class="block text-sm font-medium text-gray-700">Description</label>
        <textarea id="description" v-model="description" class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm"></textarea>
      </div>
      <button type="submit" class="w-full bg-indigo-600 text-white py-2 px-4 border border-transparent rounded-md shadow-sm text-sm font-medium hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">Submit</button>
    </form>
  </div>
</template>
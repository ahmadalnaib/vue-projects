<script>
export default {
  data() {
    return {
     
    }
  },
  methods: {
    updateFilter(by) {
      this.$emit('update-filter', by);
    }
  }
}
</script>

<template>
<div class="p-4">
  <div class="filter flex space-x-4">
    <button @click="updateFilter('all')" class="px-4 py-2 bg-blue-500 text-white rounded hover:bg-blue-700">View All</button>
    <button @click="updateFilter('Completed')" class="px-4 py-2 bg-green-500 text-white rounded hover:bg-green-700">Completed</button>
    <button @click="updateFilter('ongoing')" class="px-4 py-2 bg-yellow-500 text-white rounded hover:bg-yellow-700">Ongoing</button>
  </div>
</div>  
</template>
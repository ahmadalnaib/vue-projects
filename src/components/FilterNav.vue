<script>
export default {
  props: ['current'],

  methods: {
    updateFilter(by) {
      this.$emit('update-filter', by);
    }
  }
}
</script>

<template>
<div class="p-4">
  <div class="filter flex space-x-4 justify-center">
    <button @click="updateFilter('all')" class="px-4 py-2 bg-blue-500 text-white rounded hover:bg-blue-700" :class="{'bg-gray-600':current ==='all' }">View All</button>
    <button @click="updateFilter('completed')" class="px-4 py-2 bg-green-500 text-white rounded hover:bg-green-700" :class="{'bg-gray-600':current ==='completed' }">Completed</button>
    <button @click="updateFilter('ongoing')" class="px-4 py-2 bg-yellow-500 text-white rounded hover:bg-yellow-700" :class="{'bg-gray-600':current ==='ongoing' }">Ongoing</button>
  </div>
</div>  
</template>
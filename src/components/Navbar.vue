<script>

export default {
  name: 'Navbar',
};

</script>

<template>
  <nav>
    <div class="bg-gray-800 text-white p-5">
      <div class="container mx-auto flex justify-between">
        <router-link :to="{name:'home'}" class="text-2xl font-bold">Home</router-link>
        <router-link :to="{name:'addProject'}" class="text-2xl font-bold">Add</router-link>
      </div>
    </div>
  </nav>
</template>




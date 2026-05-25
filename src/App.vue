<script setup lang="ts">
  import {ref} from 'vue'

  const restaurantName = ref<string>('')
  const restaurants = ref<string[]>([])

  function addRestaurant() {
    const newRestaurants = [...restaurants.value, restaurantName.value]
    restaurants.value = newRestaurants
    restaurantName.value = ''
  }
</script>

<template>
  <main>
    <form @submit.prevent="addRestaurant">
      <label for="restaurant-name">Restaurant Name</label>
      <input class="input" id="restaurant-name" type="text" v-model="restaurantName"/>
      <button class="btn" type="submit">Add Restaurant</button>
    </form>
    <ul>
      <li v-for="restaurant in restaurants">{{ restaurant }}</li>
    </ul>
  </main>
</template>

<style scoped>
  .input {
    margin-left: 1rem;
  }
  .btn {
    margin-left: 0.5rem;
  }
</style>

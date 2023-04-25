<template>
  <div class="bg-white shadow rounded-xl">
    <router-link :to="{ name: 'mealDetails', params: { id: meal.idMeal } }">
      <img
        :src="meal.strMealThumb"
        :alt="meal.strMeal"
        class="rounded-t-xl w-full h-48 object-cover"
      />
    </router-link>
    <h3 class="p-3 py-2 font-semibold">{{ meal.strMeal }}</h3>
    <p class="p-3 py-2 mb-4">
      Lorem ipsum dolor sit amet consectetur adipisicing elit. Sint excepturi
      corrupti molestias optio. Quos, quaerat?
    </p>
    <div class="flex justify-between items-center p-3">
      <YoutubeButton href="meal.strYoutube"> Youtube </YoutubeButton>
    </div>
  </div>
</template>


<script setup>
import { defineProps } from "vue";

const { meal } = defineProps({
  meal: {
    required: true,
    type: Object,
  },
});
</script>
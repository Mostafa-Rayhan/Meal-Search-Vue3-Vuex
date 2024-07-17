<!-- <template>
    <div class="flex flex-col p-8">
        <input type="text"
            class="rounded border-2 border-gray-200 w-full"
            placeholder="Search for Meals"
        />

        <div class="flex justify-center gap-2 mt-2">
            <router-link :to="{name: 'byLetter', params: {letter}}" v-for="letter of letters">
                {{ letters }}
            </router-link>
        </div>

        <pre>{{ ingredients }}</pre>
    </div>
</template>

<script setup>
import { computed, onMounted, ref } from "vue";
import store from '../store';
import axiosClient from '../axiosClient.js';


//const meals = computed(() => store.state.meals)
const letters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'.split("");
const ingredients = ref([]);

onMounted(async() => {
    const response = await axiosClient.get('/list.php?i=list');
    console.log(response.data);
    ingredients.value = response.data;
})
</script> -->

<template>
  <div class="p-8 pb-0 text-orange-500">
    <h1 class="text-4xl font-bold mb-4">Random Meals</h1>
  </div>
  <Meals :meals="meals" />
</template>

<script setup>
import { computed, onMounted, ref } from "vue";
import store from "../store";
import Meals from "../components/Meals.vue";
import axiosClient from "../axiosClient.js";

const meals = ref([]);

onMounted(async () => {
  for (let i = 0; i < 10; i++) {
    axiosClient
      .get(`random.php`)
      .then(({ data }) => meals.value.push(data.meals[0]));
  }
});
</script>

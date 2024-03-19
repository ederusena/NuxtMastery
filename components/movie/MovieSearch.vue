<template>
  <!-- This example requires Tailwind CSS v2.0+ -->
  <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
    <div class="max-w-3xl mx-auto">
      <form @submit.prevent="search">
        <label for="email" class="block text-sm font-medium text-gray-700"
          >Filme</label
        >
        <div class="mt-1">
          <input
            type="text"
            name="search"
            v-model="query"
            id="email"
            class="shadow-sm p-2 focus:ring-indigo-500 focus:border-indigo-500 block w-full sm:text-sm border-gray-300 rounded-md"
            placeholder="you@example.com"
          />
        </div>
        <Divider label="+" />

        <button
          class="inline-flex items-center px-4 py-2 border border-transparent text-base font-medium rounded-md shadow-sm text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
        >
          Search
        </button>
      </form>
      <div class="bg-white">
        <div
          class="max-w-2xl mx-auto py-16 px-4 sm:py-24 sm:px-6 lg:max-w-7xl lg:px-8"
        >
          <div
            class="mt-6 grid grid-cols-1 gap-y-10 gap-x-6 sm:grid-cols-2 lg:grid-cols-4 xl:gap-x-8"
          >
            <main v-for="movie in movies" :key="movie.imdbID">
              <div class="group relative">
                <div
                  class="w-full min-h-80 bg-gray-200 aspect-w-1 aspect-h-1 rounded-md overflow-hidden group-hover:opacity-75 lg:h-80 lg:aspect-none"
                >
                  <NuxtLink
                    :to="{ name: 'movies-id', params: { id: movie.imdbID } }"
                  >
                    <img
                      :src="movie.Poster"
                      alt="Front of men&#039;s Basic Tee in black."
                      class="w-full h-full object-center object-cover lg:w-full lg:h-full"
                    />
                  </NuxtLink>
                </div>
              </div>
            </main>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
const query = ref("");
const movies = ref([]);

const search = async () => {
  const { Search } = await $fetch(
    `https://www.omdbapi.com/?i=tt3896198&apikey=a2b05f75&s=${query.value}`
  );
  movies.value = Search;
};
</script>

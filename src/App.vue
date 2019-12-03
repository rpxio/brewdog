<template>
  <div id="app" class="font-sans mt-4 p-6">
    <div class="mb-12 flex items-center justify-center">
      <h1>Find Your New Favorite Beer!</h1>
    </div>

    <div class="mb-8 flex items-center justify-center">
      <form @submit.prevent="search">
        <div class="flex border border-gray-400 rounded overflow-hidden">
          <input
            v-model="query"
            type="search"
            class="px-4 py-2 text-gray-700"
          />
          <button
            type="submit"
            class="items-center justify-center px-4 my-1 border-l"
          >
            <svg
              class="fill-current text-gray-500 h-4 w-4"
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 24 24"
            >
              <path
                d="M16.32 14.9l5.39 5.4a1 1 0 0 1-1.42 1.4l-5.38-5.38a8 8 0 1 1 1.41-1.41zM10 16a6 6 0 1 0 0-12 6 6 0 0 0 0 12z"
              />
            </svg>
          </button>
        </div>
        <input type="radio" v-model="option" value="beer_name" checked /> Name
        <input type="radio" v-model="option" value="food" /> Food
      </form>
    </div>

    <div class="mb-6 flex items-center justify-center">
      <div v-if="searching" class="font-bold">Searching...</div>

      <div v-if="noResults" class="font-bold">Sorry. No results found.</div>

      <div v-if="count" class="font-bold">{{ count }} Results Found</div>
    </div>

    <div class="container mx-auto">
      <div class="flex flex-wrap -mb-4">
        <div
          class="sm:w-full md:w-1/3 m-1 p-4 border shadow rounded"
          v-for="result in results"
          :key="result.id"
        >
          <img class="h-32" :src="result.image_url" />
          <br />
          <div class="font-bold mb-2">
            {{ result.name }}
            <span class="text-gray-700"
              >{{ result.first_brewed }} | {{ result.abv }}</span
            >
          </div>
          <p class="text-gray-700 text-base">{{ result.description }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'app',
  data() {
    return {
      query: '',
      results: [],
      noResults: false,
      searching: false,
      count: '',
      option: 'beer_name'
    }
  },
  methods: {
    search: function() {
      this.count = ''
      this.results = []
      this.searching = true
      this.noResults = false

      axios
        .get(
          `https://api.punkapi.com/v2/beers?` +
            this.option +
            `=${encodeURIComponent(this.query)}`
        )
        .then(res => {
          if (res.data.length === 0) {
            this.noResults = true
          }

          this.searching = false
          this.results = res.data
          this.count = res.data.length
        })
    }
  }
}
</script>

<template>
  <div id="app">
    <form @submit.prevent="search">
      <input v-model="query" type="search" />
      <button type="submit">Search</button>
    </form>
    <br />

    <div v-if="searching">
      <i>Searching...</i>
    </div>

    <div v-if="noResults">Sorry. No results found.</div>

    <div v-for="result in results" :key="result.id">
      <div>
        <img class="h-32" :src="result.image_url" />
        <br />
        <div class="px-6 py-4">
          <div class="font-bold mb-2">{{ result.name }}</div>
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
      searching: false
    }
  },
  methods: {
    search: function() {
      this.results = []
      this.searching = true

      axios
        .get(
          `https://api.punkapi.com/v2/beers?beer_name=${encodeURIComponent(
            this.query
          )}`
        )
        .then(res => {
          this.searching = false
          this.results = res.data
        })
    }
  }
}
</script>

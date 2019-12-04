<template>
  <div id="app" class="font-sans mt-4 p-4">
    <div class="mb-12 flex items-center justify-center">
      <h1>Find Your New Favorite Beer!</h1>
    </div>

    <div class="mb-8 flex items-center justify-center">
      <form @submit.prevent="search">
        <div class="flex border border-gray-400 rounded overflow-hidden mb-2">
          <input
            v-model="query"
            type="search"
            placeholder=""
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
        <div class="flex justify-around pb-2 mb-2 border-b">
          <div>
            <input
              id="opt1"
              type="radio"
              v-model="option"
              value="beer_name"
              checked
            />
            <label for="opt1"> Beer Name</label>
          </div>
          <div>
            <input id="opt2" type="radio" v-model="option" value="food" />
            <label for="opt2"> Food Pairing</label>
          </div>
        </div>
        <div class="flex justify-center">
          <span>Sort By: </span>
          <select v-model="sortProp">
            <option value="id">None</option>
            <option value="name">Beer Name</option>
            <option value="first_brewed">First Brew Date</option>
            <option value="abv">ABV</option>
          </select>
        </div>
      </form>
    </div>

    <div class="mb-6 flex items-center justify-center">
      <div v-if="searching" class="font-bold">Searching...</div>

      <div v-if="noResults" class="font-bold">Sorry. No results found.</div>

      <div v-if="count" class="font-bold">{{ count }} Results Found</div>

      <div
        v-if="noQuery"
        class="font-bold bg-red-500 text-white px-2 py-1 rounded"
      >
        Please enter a search term.
      </div>

      <div
        v-if="searchError"
        class="font-bold bg-red-500 text-white px-2 py-1 rounded"
      >
        {{ errorContents }}. Please try again.
      </div>
    </div>

    <div class="container mx-auto">
      <div class="flex flex-wrap -mx-2 mb-8 justify-center">
        <div
          class="max-w-md lg:w-1/2 px-2 mb-4"
          v-for="result in orderedResults"
          :key="result.id"
        >
          <div class="shadow rounded-lg border border-gray-200 overflow-hidden">
            <div class="h-40 flex justify-center">
              <div
                class="p-2 ml-4 mt-4 h-32 w-32 rounded-full bg-blue-200 flex justify-center overflow-hidden"
              >
                <img
                  class="max-h-full"
                  :src="result.image_url || './img/blank.png'"
                  alt
                />
              </div>
            </div>
            <div class="border-t-4 border-blue-200 p-6">
              <h2
                class="text-gray-700 tracking-tight leading-tight text-3xl font-medium mb-4"
              >
                {{ result.name }}
              </h2>
              <div class="my-4 flex items-center">
                <div class="w-1/2">
                  <h3 class="text-gray-700 text-2xl font-bold -mb-1 -pb-1">
                    {{ result.first_brewed }}
                  </h3>
                  <p
                    class="text-gray-600 text-xs uppercase tracking-widest mt-0 pt-0"
                  >
                    First Brewed
                  </p>
                </div>
                <div class="w-1/2">
                  <h3 class="text-gray-700 text-2xl font-bold -mb-1 -pb-1">
                    {{ result.abv }}
                  </h3>
                  <p
                    class="text-gray-600 text-xs uppercase tracking-widest mt-0 pt-0"
                  >
                    ABV
                  </p>
                </div>
              </div>
              <p class="text-gray-900">{{ result.description }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// import MessageBox from '@/components/MessageBox.vue'
import axios from 'axios'
import _ from 'lodash'

export default {
  name: 'app',
  data() {
    return {
      query: '',
      results: [],
      noResults: false,
      searching: false,
      noQuery: false,
      count: '',
      option: 'beer_name',
      searchError: false,
      errorContents: '',
      sortProp: 'id'
    }
  },
  methods: {
    search: function() {
      this.count = ''
      this.results = []
      this.noResults = false
      this.searchError = false

      if (this.query.length === 0) {
        this.noQuery = true
      } else {
        this.noQuery = false
        this.searching = true

        axios
          .get(
            `https://api.punkapi.com/v2/beers?` +
              this.option +
              `=${encodeURIComponent(this.query)}`
          )
          .then(
            res => {
              if (res.data.length === 0) {
                this.noResults = true
              }

              this.searching = false
              this.results = res.data
              this.count = res.data.length
            },
            error => {
              this.searching = false
              this.searchError = true
              this.errorContents = error
            }
          )
      }
    }
  },
  computed: {
    orderedResults: function() {
      return _.orderBy(this.results, this.sortProp)
    }
  }
}
</script>

<template>
  <section class="container mx-auto">

    <div class="justify-center float-none">
      <div class="flex flex-col text-center w-full py-24">
        <h1 class="sm:text-3xl text-2xl font-medium title-font mb-4 text-gray-900">Welcome to NASA Application
        </h1>
        <p class="lg:w-2/3 mx-auto leading-relaxed text-base">You can search for any space image of your choice and it will be displayed to
          you.</p>
      </div>
      <form>
        <div class="container px-5 py-4 mx-auto">
          <div
            class="flex lg:w-2/3 w-full sm:flex-row flex-col mx-auto px-8 sm:space-x-4 sm:space-y-0 space-y-4 sm:px-0 items-end">
            <div class="relative flex-grow w-full">
              <label for="email" class="leading-7 text-sm text-gray-600"></label>
              <input type="email" id="search-bar" placeholder="Search for NASA Images "
                class="w-full bg-gray-100 bg-opacity-50 rounded border border-gray-300 focus:border-indigo-500 focus:bg-transparent focus:ring-2 focus:ring-indigo-200 text-base outline-none text-gray-700 py-3 px-3 leading-8 transition-colors duration-200 ease-in-out"
                v-model="query">
            </div>
            <button class="text-white bg-btn border-0 py-2 px-12 focus:outline-none rounded text-sm"
              @click.prevent="fetchResults">Search
              Images</button>
          </div>
        </div>
      </form>

      <div class="flex flex-wrap -m-4">
        <div class="lg:w-1/3 sm:w-1/2 p-4" v-for="result in results">
          <div class="flex relative">
            <img alt="gallery" class="absolute inset-0 w-full h-full object-cover object-center"
              :src="result.links[0].href">
            <div class="px-8 py-10 relative z-10 w-full border-4 border-gray-200 bg-white opacity-0 hover:opacity-100">
              <h2 class="tracking-widest text-sm title-font font-medium text-indigo-500 mb-1">{{ result.data[0].title }}
              </h2>
              <h1 class="title-font text-lg font-medium text-gray-900 mb-3" v-for="keyword in result.data[0].keywords">
                <span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2">{{
                  keyword }}</span>
              </h1>

            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
<script lang="ts">
import axios from 'axios'
export default {
  name: "Counter",
  data() {
    return {
      results: [],
      query: ""
    }
  },
  methods: {
    fetchResults: function () {
      axios.get(`https://images-api.nasa.gov/search?q=${this.query}&media_type=image`,)
        .then((response) => {
          return response.data
        })
        .then((parsedJson) => {
          this.results = parsedJson["collection"]["items"];
        })
    }
  }
}
</script>
<style>
@import url('https://fonts.googleapis.com/css2?family=Work+Sans&display=swap');

.bg-btn {
  background-color: #3C9521;
}

.container {
  font-family: 'Work Sans', sans-serif;
}
</style>
    

    

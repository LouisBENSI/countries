<template>

  <main class="max-w-[1280px] px-4 mx-auto xl:px-0 dark:bg-gray-800">

    <div class="flex flex-col justify-between my-12 md:flex-row">
      <input v-model="search" type="text" class="w-full h-[40px] md:max-w-[500px] border-gray-300 pl-4  rounded-md md:mr-2" placeholder="Rechercher un pays">
      <select v-model="selected" class="mt-1 block w-full pl-3 py-2 text-base border-gray-300 rounded-md focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 cursor-pointer sm:text-sm md:mt-0 md:ml-2 md:w-[300px]">
        <option disabled value="">Chosissez la région</option>
        <option value="africa">Afrique</option>
        <option value="americas">Amérique</option>
        <option value="asia">Asie</option>
        <option value="europe">Europe</option>
        <option value="oceania">Océanie</option>
        <option value="all">Toutes les régions</option>
      </select>
    </div>

    <!-- CONTAINER COUNTRIES -->
    <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-4 sm:gap-6 md:gap-8">

      <!-- LOADER -->
      <div v-if="loading">
        <img src="/src/assets/loader/pulse.gif" alt="">
      </div>

      <!-- COUNTRY -->
      <div v-else v-for="country in countries.sort((a, b) => a.name.common.localeCompare(b.name.common))" :key="country.id" class="w-full rounded-md overflow-hidden shadow border border-solid border-gray-200">
        <!-- IMG -->
        <div class="bg-gray-400 h-48 w-full">
          <img :src="country.flags.svg" alt="" class="w-full h-full object-cover">
        </div>
        <!-- CONTENT -->
        <div class="p-4 pb-8 bg-white">
          <p class="text-gray-800 font-bold">{{ country.translations.fra.common }}</p>
          <ul class="mt-4 text-sm space-y-1 text-gray-600">
            <li><strong>Population</strong> : {{ Number(country.population).toLocaleString().split(/\s/).join(', ') }} habitants</li>
            <li><strong>Region</strong> : {{ country.region }}</li>
            <li v-for="cap in country.capital" :key="cap.id"><strong>Capital</strong> : {{ cap }}</li>
          </ul>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  data() {
    return {
      countries: [],
      search: '',
      selected: '',

      loading: false,
    }
  },

  created() {
    this.displayCountriesAll()
  },

  methods: {
    displayCountriesAll() {
      this.loading = !this.loading
      let url = "https://restcountries.com/v3.1/all"
      fetch(url)
          .then(res => res.json())
          .then(data => this.countries = data)
      this.loading = !this.loading
    },
  },

  watch: {

    search() {
      if (this.selected == "all" && this.selected.length < 3) {
        this.displayCountriesAll()
      } else {
        let url = `https://restcountries.com/v3.1/name/${this.search}`
        fetch(url)
            .then(res => res.json())
            .then(data => this.countries = data)
      }
    },

    selected() {
      if (this.selected == "all") {
        this.displayCountriesAll()
      } else {
        let url = `https://restcountries.com/v3.1/region/${this.selected}`
        fetch(url)
            .then(res => res.json())
            .then(data => this.countries = data)
      }
    }
  },

  name: 'Main',
}
</script>
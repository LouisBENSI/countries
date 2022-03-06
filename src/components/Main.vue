<template>

  <main class="max-w-[1280px] mx-auto dark:bg-gray-800">

    <div class="flex justify-between mt-12">
      <div>
        <input @change="onChangeSearch()" v-model="search" type="text" class="h-[40px] w-[500px] pl-4 shadow rounded-md" placeholder="Rechercher un pays">
      </div>

      <div>
        <select @change="onChange()" v-model="selected" id="location" name="location" class="mt-1 block w-full pl-3 pr-10 py-2 text-base border-gray-300 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm rounded-md">
          <option value="all" selected>Choisissez la région</option>
          <option value="africa">Afrique</option>
          <option value="americas">Amérique</option>
          <option value="asia">Asie</option>
          <option value="europe">Europe</option>
          <option value="oceania">Océanie</option>
        </select>
      </div>
    </div>

    <!-- CONTAINER COUNTRIES -->
    <div class="mt-12 md:flex md:flex-wrap justify-between">
      <!-- COUNTRY -->
      <div v-for="country in countries" :key="country.id" class="w-[275px] mb-12 rounded-md overflow-hidden shadow border border-solid border-gray-200">
        <!-- IMG -->
        <div class="bg-gray-400 h-48 w-full">
          <img :src="country.flags.svg" alt="" class="w-full h-full object-cover">
        </div>
        <!-- CONTENT -->
        <div class="p-4 pb-8 bg-white">
          <p class="text-gray-800 font-bold">{{ country.translations.fra.common }}</p>
          <ul class="mt-4 text-sm space-y-1 text-gray-600">
            <li><strong>Population</strong> : {{ country.population }}</li>
            <li><strong>Region</strong> : {{ country.region }}</li>
            <li><strong>Capital</strong> : {{ country.capital }}</li>
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
    }
  },
  methods: {
    onChange() {
      let url = "https://restcountries.com/v3.1/region/" + this.selected;
      fetch(url)
          .then(res => res.json())
          .then(data => this.countries = data);
    },
    onChangeSearch() {
      let url = "https://restcountries.com/v3.1/name/" + this.search;
      fetch(url)
          .then(res => res.json())
          .then(data => this.countries = data);
    },
  },
  mounted() {
    let url = "https://restcountries.com/v3.1/all";
    fetch(url)
        .then(res => res.json())
        .then(data => this.countries = data);
  }
  ,
  name: 'Main',
}
</script>
<template>
  <main class="container">
    <TitleAndTime :text="title" :dataDate="dataDate" />

    <CovidData :stats="stats" />

    <div v-if="stats.Country" class="box">
      <h3>Active Cases</h3>
        <div>
          {{ numWithCommas(countryActiveCases) }}
        </div>
    </div>

    <SelectCountry @get-country="getCountry" :countries="countries" /> <br><br>

    <button @click="reloadPage" v-if="stats.Country" class="button">Current summary</button>
  </main>
</template>

<script>
import TitleAndTime from '@/components/TitleAndTime'
import CovidData from '@/components/CovidData'
import SelectCountry from '@/components/SelectCountry'

export default {
  name: 'HomeView',
  components: {
    TitleAndTime,
    CovidData,
    SelectCountry,
  },
  data() {
    return {
      title: 'Current summary',
      dataDate: '',
      stats: {},
      countries: [],
      countryActiveCases: null
    }
  },
  methods: {
    async covidSummary() {
      const url = ('https://api.covid19api.com/summary')
      const results = await fetch(url)
      const renderResults = await results.json()
      return renderResults
    },

    async activeCases(countrySlug) {
      let d = new Date()
      d.setDate(d.getDate() - 1)
      
      const url = (`https://api.covid19api.com/live/country/${countrySlug}/status/confirmed/date/${d.toISOString()}`)
      const results = await fetch(url)
      const renderResults = await results.json()
      this.countryActiveCases = renderResults.reduce((sum, it) => sum + it.Active, 0)
    },

    getCountry(country) {
      this.stats = country
      this.title = country.Country
      this.activeCases(country.Slug)
    },
    reloadPage() {
      window.location.reload()
    },

    numWithCommas(x) {
      return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, '.');
    }

  },
  
  async created() {
    const data = await this.covidSummary()
    
    this.dataDate = data.Date
    this.stats = data.Global
    this.countries = data.Countries

  },
}
</script>

<style>
.box{
    border: 2px solid;
    padding: 2px;
    margin: 5px;
    width: 250px;
    text-align: center;
}
.container{
  padding: 2px;
  margin: 5px;
}
.button{
  padding: 2px;
  margin: 5px;
}

</style>
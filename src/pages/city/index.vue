<template>
  <div>
    <city-header></city-header>
    <city-search :cities="cities"></city-search>
    <city-list :alphabet="alphabet" :cities="cities" :hotCities="hotCities"></city-list>
    <city-alphabet @change="changeAlphabet" :cities="cities"></city-alphabet>
  </div>
</template>

<script>
import CityHeader from './components/Header'
import CitySearch from './components/Search'
import CityList from './components/list'
import CityAlphabet from './components/Alphabet'
import axios from 'axios'

export default {
  name: 'City',
  components: {
    CityHeader,
    CitySearch,
    CityList,
    CityAlphabet
  },
  data () {
    return {
      hotCities: [],
      cities: {},
      alphabet: ''
    }
  },
  mounted () {
    this.getCityList()
  },
  methods: {
    getCityList () {
      axios.get('/api/city.json')
        .then(res => {
          const data = res.data.data
          this.hotCities = data.hotCities
          this.cities = data.cities
        })
    },
    changeAlphabet (e) {
      this.alphabet = e
    }
  }
}
</script>

<style lang="stylus" scoped>

</style>

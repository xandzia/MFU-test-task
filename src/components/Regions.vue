<template>
  <div class="regions">
    <h1>{{ msg }}</h1>
<!--    <button v-on:click.prevent="getResult()">Search</button>-->
    <select v-model="selected"
       v-on:click="emit"
       v-on:change="myMethod()">
       <option disabled value="">List of regions</option>
        <option v-for="region in regions" 
        :key="region.regionCode" 
        :value="region.regionCode">{{ region.regionName }}</option>
    </select>
      <span>{{ selected }}</span>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'regions',
  data () {
    return {
      msg: 'regions',
      selected: '',
      regions: null
    }
  },
  created () {
    this.getResult()
  },
  methods: {
    myMethod () {
      axios('http://api.spending.gov.ua/api/v2/api/transactions/top100?region='+this.selected, { method: 'GET', mode: 'no-cors' })
        .then((response) => {
          console.log('transactions', response.data)
        })
        .catch((error) => {
          console.log('err', error)
        })
    },
    getResult () {
      axios('http://api.spending.gov.ua/api/v2/regions', { method: 'GET', mode: 'no-cors' })
        .then((response) => {
          response.data.shift()
          this.regions = response.data
          console.log(this.regions)
        })
        .catch((error) => {
          console.log('err', error)
        })
    },
    emit () {
      this.$emit('event_child', this.selected)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
h1, h2 {
  font-weight: normal;
}
a {
  color: #42b983;
}
</style>

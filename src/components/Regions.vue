<template>
  <div class="regions">
    <h1>{{ msg }}</h1>
<!--    <button v-on:click.prevent="getResult()">Search</button>-->
    <select v-model="info.regionId" v-on:click="emit" v-on:change="getTransactions()">
       <option disabled value="">List of regions</option>
        <option v-for="region in regions" :key="region.regionCode" :value="region.regionCode">{{ region.regionName }}</option>
    </select>
      <span>{{ info.regionId }}</span>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'regions',
  data () {
    return {
      msg: 'regions',
      info: {
        regionId: '',
        transactions: []
      },
      regions: null
    }
  },
  created () {
    this.getRegions()
  },
  methods: {
    getTransactions () {
      axios('http://api.spending.gov.ua/api/v2/api/transactions/top100?region=' + this.info.regionId, { method: 'GET', mode: 'no-cors' })
        .then((response) => {
          let arr = []
          for (let i = 0; i < response.data.length; i++) {
            arr.push(response.data[i].amount)
          }
          this.info.transactions = arr
          console.log('transactions', response.data)
        })
        .catch((error) => {
          console.log('err', error)
        })
    },
    getRegions () {
      this.getResult('http://api.spending.gov.ua/api/v2/regions')
    },
    getResult (api) {
      axios(api, { method: 'GET', mode: 'no-cors' })
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
      this.$emit('event_child', this.info)
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

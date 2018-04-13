<template>
  <div class="transactions">
    <h1>{{ msg }}</h1>
    <h1>{{ regionId }}</h1>
    <ul>
<!--        <li v-for="transaction in transactions"></li>-->
    </ul>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'transactions',
  props: {
      regionId: {
          type: Number,
          required: 2
      }
  },
  data () {
    return {
      msg: 'transactions',
      regions: null
    }
  },
  created () {
    this.getResult()
  },
  methods: {
    getResult () {
      axios('http://api.spending.gov.ua/api/v2/api/transactions/top100?region='+this.regionId, { method: 'GET', mode: 'no-cors' })
        .then((response) => {
          console.log('transactions', response.data)
          console.log('props', this.regionId)
        })
        .catch((error) => {
          console.log('err', error)
        })
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

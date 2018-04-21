<template>
  <b-container>
    <h1>{{ msg }}</h1>
    <div md="6" sm="12" class="forDown">
      <select class="select" v-model="info.regionId" v-on:click="emit" v-on:change="getTransactions()">
        <option disabled value="">Список регіонів</option>
        <option v-for="region in regions" :key="region.regionCode" :value="region.regionCode">{{ region.regionName }}
        </option>
      </select>
      <span class="down">&#x25BC;</span>
      <img class="loader" v-show="loader" src="../assets/30.gif" alt="loader">
    </div>
  </b-container>
</template>

<script>
import axios from 'axios'

export default {
  name: 'regions',
  data () {
    return {
      msg: 'Регіони',
      loader: true,
      info: {
        regionId: '',
        transactions: [],
        january: [],
        february: [],
        march: [],
        april: [],
        may: [],
        june: [],
        july: [],
        august: [],
        september: [],
        october: [],
        november: [],
        december: []
      },
      regions: null
    }
  },
  created () {
    this.getRegions()
  },
  methods: {
    getTransactions () {
      this.loader = true
      axios('https://thingproxy.freeboard.io/fetch/http://api.spending.gov.ua/api/v2/api/transactions/top100?region=' + this.info.regionId, {
        method: 'GET',
        mode: 'no-cors'
      })
        .then((response) => {
          this.loader = false
          let arr = []
          for (let i = 0; i < 100; i++) {
            let graf = []
            graf.push(response.data[i].trans_date)
            let sum = parseInt(response.data[i].amount)
            graf.push(sum)
            arr.push(graf)
          }
          arr = arr.sort(this.sortArrays)
          Promise.all(this.sumSameDays(arr)).then((arr) => {
            this.info.transactions = arr
          })
        })
        .catch((error) => {
          console.log('err', error)
        })
    },
    getRegions () {
      this.loader = true
      axios('https://thingproxy.freeboard.io/fetch/http://api.spending.gov.ua/api/v2/regions', {
        method: 'GET',
        mode: 'no-cors'
      })
        .then((response) => {
          this.loader = false
          response.data.shift()
          this.regions = response.data
        })
        .catch((error) => {
          console.log('err', error)
        })
    },
    sortArrays (a, b) {
      if (a[0] < b[0]) return -1
      if (a[0] > b[0]) return 1
      return 0
    },
    changeDate (arr) {
      arr = arr.sort(this.sortArrays)
      console.log(arr)
      for (let i = 0; i < arr.length; i++) {
        let date = new Date(arr[i][0])
        let day = date.getDate()
        let month = date.getMonth() + 1
        if (month === 1) {
          month = 'Січ'
          this.info.january.push(arr[i])
        } else if (month === 2) {
          month = 'Лют'
          this.info.february.push(arr[i])
        } else if (month === 3) {
          month = 'Берез'
          this.info.march.push(arr[i])
        } else if (month === 4) {
          month = 'Квіт'
          this.info.april.push(arr[i])
        } else if (month === 5) {
          month = 'Трав'
          this.info.may.push(arr[i])
        } else if (month === 6) {
          month = 'Черв'
          this.info.june.push(arr[i])
        } else if (month === 7) {
          month = 'Лип'
          this.info.july.push(arr[i])
        } else if (month === 8) {
          month = 'Серп'
          this.info.august.push(arr[i])
        } else if (month === 9) {
          month = 'Верес'
          this.info.september.push(arr[i])
        } else if (month === 10) {
          month = 'Жовт'
          this.info.october.push(arr[i])
        } else if (month === 11) {
          month = 'Лист'
          this.info.november.push(arr[i])
        } else if (month === 12) {
          month = 'Груд'
          this.info.december.push(arr[i])
        }
        arr[i][0] = day + ' ' + month
      }
    },
    sumSameDays (arr) {
      const newArray = []
      newArray.push(arr.reduce((acc, value) => {
        if (acc[0] !== value[0]) {
          newArray.push(acc)
          acc = [value[0], 0]
        }
        return [value[0], acc[1] + value[1]]
      }))
      this.changeDate(newArray)
      console.log(newArray)
      return newArray
    },
    emit () {
      this.$emit('event_child', this.info)
    }
  }
}
</script>

<style lang="scss" scoped>
  h1, h2 {
    font-weight: normal;
  }

  a {
    color: #42b983;
  }

  .forDown {
    position: relative;
  }

  .down {
    position: absolute;
    top: 7px;
    right: 7px;
  }

  .loader {
    position: absolute;
    bottom: -9em;
    left: 50%;
    transform: translate(-50%, 150%);
  }

  .select {
    display: inline-block;
    width: 100%;
    height: calc(2.25rem + 2px);
    padding: 0.375rem 1.75rem 0.375rem 0.75rem;
    line-height: 1.5;
    color: #495057;
    vertical-align: middle;
    background-size: 8px 10px;
    border: 1px solid #ced4da;
    border-radius: 0.25rem;
    -webkit-appearance: none;
  }
</style>

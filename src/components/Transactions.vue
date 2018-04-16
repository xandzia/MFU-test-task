<template>
  <b-container>
    <h1>{{ msg }}</h1>
    <column-chart :data="but" label="sum" suffix="грн" :messages="{empty: 'No data'}" thousands="," :library="{backgroundColor: '#eee'}" :colors="['#3ca745', '#3ca744']"></column-chart>
    <div md="6" sm="12">
      <b-button variant="outline-secondary" size="sm" @click="january()">Січень</b-button>
      <b-button variant="outline-secondary" size="sm" @click="february()">Лютий</b-button>
      <b-button variant="outline-secondary" size="sm" @click="march()">Березень</b-button>
      <b-button variant="outline-secondary" size="sm" @click="april()">Квітень</b-button>
      <b-button variant="outline-secondary" size="sm" @click="may()">Травень</b-button>
      <b-button variant="outline-secondary" size="sm" @click="june()">Червень</b-button>
      <b-button variant="outline-secondary" size="sm" @click="july()">Липень</b-button>
      <b-button variant="outline-secondary" size="sm" @click="august()">Серпень</b-button>
      <b-button variant="outline-secondary" size="sm" @click="september()">Вересень</b-button>
      <b-button variant="outline-secondary" size="sm" @click="october()">Жовтень</b-button>
      <b-button variant="outline-secondary" size="sm" @click="november()">Листопад</b-button>
      <b-button variant="outline-secondary" size="sm" @click="december()">Грудень</b-button>
    </div>
  </b-container>
</template>
<script>
import Vue from 'vue'
import VueChartkick from 'vue-chartkick'
// import Chart from 'chart.js'

Vue.use(VueChartkick)
export default {
  name: 'transactions',
  data () {
    return {
      msg: 'Транзакції',
      but: null
    }
  },
  props: {
    infoData: null
  },
  watch: {
    'infoData.transactions': function () {
      this.but = this.infoData.transactions
    }
  },
  methods: {
    february () {
      this.but = this.infoData.february
    },
    january () {
      this.but = this.infoData.january
    },
    april () {
      this.but = this.infoData.april
    },
    march () {
      this.but = this.infoData.march
    },
    may () {
      this.but = this.infoData.may
    },
    june () {
      this.but = this.infoData.june
    },
    july () {
      this.but = this.infoData.july
    },
    august () {
      this.but = this.infoData.august
    },
    september () {
      this.but = this.infoData.september
    },
    october () {
      this.but = this.infoData.october
    },
    november () {
      this.but = this.infoData.november
    },
    december () {
      this.but = this.infoData.december
    },
    separation (arr) {
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

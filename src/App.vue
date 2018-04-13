<template>
  <div id="app">
<!--    <img src="./assets/logo.png">-->
   <regions v-on:event_child="getIdFromRegions"></regions>
   <transactions :regionId="id"></transactions>
  </div>
</template>

<script>
import Regions from './components/Regions'
import Transactions from './components/Transactions'
export default {
  name: 'App',
  data () {
    return {
      id: 2
    }
  },
  components: {
    Regions,
    Transactions
  },
  methods: {
    getIdFromRegions (id) {
      this.id = id
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

<template>
  <div id="app" >
<!--    <img src="./assets/logo.png">-->
   <a class="print" href="javascript:window.print()" label="print"><span>&#128438;</span></a>
   <regions v-on:event_child="eventChild"></regions>
   <transactions :infoData="data"></transactions>
   <mapdraw :infoData="data"></mapdraw>
  </div>
</template>

<script>
import Regions from './components/Regions'
import Transactions from './components/Transactions'
import Mapdraw from './components/Mapdraw'
import 'bootstrap/dist/css/bootstrap.css'
import 'bootstrap-vue/dist/bootstrap-vue.css'
export default {
  name: 'App',
  data () {
    return {
      data: null
    }
  },
  components: {
    Regions,
    Transactions,
    Mapdraw
  },
  methods: {
    eventChild (data) {
      this.data = data
      console.log('data', this.data)
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
  color: #212529;
  margin-top: 60px;
}
.print {
  color: #6c757d;
  font-size: 2em;
  position: absolute;
  top: 20px;
  right: 20px;
}
.print:hover,
.print:active {
  text-decoration: none;
  color: #3d7bff;
}
</style>

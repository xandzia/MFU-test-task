<template>
  <div class="transactions">
    <h1>{{ msg }}</h1>
    <p>{{ infoData }}</p>
    <ul>
<!--        <li v-for="transaction in transactions"></li>-->
    </ul>
  </div>
</template>

<script>
export default {
  name: 'transactions',
  props: {
    infoData: {
      type: Object,
      required: true
    }
  },
  data () {
    return {
      msg: 'transactions'
    }
  },
  methods: {
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

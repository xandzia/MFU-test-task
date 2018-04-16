<template>
   <b-container>
   <b-button variant="outline-secondary" size="sm" @click="amount(infoData.transactions)">Мапа</b-button>
    <div v-show="hideMap" id="visualization" style="margin: 1em"></div>
   </b-container>
</template>

<script>
export default {
  name: 'mapdraw',
  data () {
    return {
      hideMap: false,
      sum: '0'
    }
  },
  props: {
    infoData: null
  },
  created () {
    this.initMap()
  },
  methods: {
    amount (arr) {
      let count = 0
      for (let i = 0; i < arr.length; i++) {
        count += parseInt(arr[i][1])
      }
      this.sum = toString(count)
      this.hideMap = true
    },
    initMap () {
      window.google.load('visualization', '1', {'packages': ['geochart']})
      window.google.setOnLoadCallback(drawVisualization)
      function drawVisualization () {
        let data = window.google.visualization.arrayToDataTable([
          ['Region', 'Sum'],
          ['UA-32', '199581477'], // kiev
          ['UA-43', '199581477'], // krim
          ['UA-30', '199581477'], // KIEV
          ['UA-18', '199581477'], // zytom
          ['UA-07', '199581477'], // volun
          ['UA-46', '199581477'], // lviv
          ['UA-56', '199581477'], // rivne
          ['UA-21', '199581477'], // zakar
          ['UA-26', '199581477'], // if
          ['UA-77', '199581477'], // chernivci
          ['UA-61', '199581477'], // ternop
          ['UA-68', '199581477'], // xmeln
          ['UA-05', '199581477'], // vinnuc
          ['UA-71', '199581477'], // cherk
          ['UA-35', '199581477'], // kirovo
          ['UA-51', '199581477'], // odes
          ['UA-48', '199581477'], // mykolaiv
          ['UA-74', '199581477'], // chernigiv
          ['UA-59', '199581477'], // summ
          ['UA-53', '199581477'], // polt
          ['UA-63', '199581477'], // xarkiv
          ['UA-12', '199581477'], // dniprop
          ['UA-09', '199581477'], // luxansk
          ['UA-14', '199581477'], // doneck
          ['UA-23', '199581477'], // zapor
          ['UA-65', '199581477'] // xerson
        ])
        let opts = {
          region: 'UA',
          displayMode: 'regions',
          resolution: 'provinces',
          width: 640,
          height: 480
        }
        let geochart = new window.google.visualization.GeoChart(document.getElementById('visualization'))
        geochart.draw(data, opts)
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>

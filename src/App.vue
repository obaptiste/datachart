<template>
<div class="small">
  <line-chart :chart-data="datacollection"></line-chart>
  <button @click="andRepeat()">Randomize</button>
</div>
</template>

<script>
import LineChart from './components/LineChart.js'

export default {
  components: {
    LineChart
  },
  data () {
    return {
      datacollection: null,
      dataOne: null,
      dataTwo: null,
      labels: null,
      options: null
    }
  },
  mounted () {
    this.labels = ['1', '2', '3', '4', '5', '6', '7', '8', '9', '10']
    this.dataOne = [25, 10, 11, 23, 36, 44, 66, 20, 11, 50, 7]
    this.dataTwo = [40, 10, 1, 5, 20, 44, 13, 30, 5, 29, 44]
    this.fillData()

  },
  methods: {
    fillData () {
      this.datacollection = {
        labels: this.labels,
        datasets: [
          {
            label: 'Data One',
            backgroundColor: 'green',
            data: this.dataOne
          }, {
            label: 'Data Two',
            backgroundColor: 'blue',
            data: this.dataTwo
          }
        ]
      }
    },
    getRandomInt () {
      return Math.floor(Math.random() * (50 - 5 + 1)) + 5
    },
    doOnePoint () {
      var x = this.getRandomInt()
      this.dataOne.push(x)
    },
    doTwoPoint () {
      var y = this.getRandomInt()
      this.dataTwo.push(y)
    },
    updateLabels () {
      var z = this.dataOne.length.toString()
      this.labels.push(z)
    },
    doPointUpdate () {
      this.doOnePoint()
      this.doTwoPoint()
      this.updateLabels()
      this.fillData()
    },
    andRepeat () {
      setInterval(() => {
        this.doPointUpdate()
      }, 1000)
    }
  }
}
</script>

<style>
.small {
  max-width: 600px;
  margin:  150px auto;
}
</style>

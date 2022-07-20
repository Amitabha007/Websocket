<template>
  <div class="small">
    <line-chart :chart-data="datacollectionChart1" id="mychart1"></line-chart>
    <line-chart :chart-data="datacollectionChart2" id="mychart2"></line-chart>
  </div>
</template>
    
<script>
import LineChart from "../LineChart.js";
import io from "socket.io-client";
var socket = io.connect("http://localhost:4000");
    
export default {
  components: {
    LineChart
  },
  data: function() {
    return {
      datacollectionChart1: null,
      datacollectionChart2: null
    };
  },
  created: function() {
    this.getRealtimeDataChart1()
  },
  methods: {
    fillData(fetchedData) {
      this.datacollectionChart1 = {
        labels: [this.getRandomChartValues(fetchedData), this.getRandomChartValues(fetchedData)],
        datasets: [
          {
            label: "Google Stock",
            backgroundColor: "#1A73E8",
            data: [this.getRandomChartValues(fetchedData), this.getRandomChartValues(fetchedData)]
          },
          {
            label: "Microsoft Stock",
            backgroundColor: "#2b7518",
            data: [this.getRandomChartValues(fetchedData), this.getRandomChartValues(fetchedData)]          }
        ]
      };
    },
    fillData1(fetchedData) {
      this.datacollectionChart2 = {
        labels: [this.getRandomChartValues(fetchedData), this.getRandomChartValues(fetchedData)],
        datasets: [
          {
            label: "Google Stock",
            backgroundColor: "#1A73E8",
            data: [this.getRandomChartValues(fetchedData), this.getRandomChartValues(fetchedData)]
          },
          {
            label: "Microsoft Stock",
            backgroundColor: "#2b7518",
            data: [this.getRandomChartValues(fetchedData), this.getRandomChartValues(fetchedData)]          }
        ]
      };
    },
    getRealtimeDataChart1() {
      console.log('test connection')
      socket.on("newdata", fetchedData => {
        this.fillData(fetchedData) 
      })
      socket.on("newdata1", fetchedData => {
        this.fillData1(fetchedData) 
      })
    },
    getRandomChartValues(number){
      return Math.floor(Math.random() * number)
    }
  }
};
</script>
<style>
.small {
  max-width: 600px;
  margin: 150px auto;
}
</style>
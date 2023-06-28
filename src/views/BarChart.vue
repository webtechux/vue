<template>
  <div class="bar">
    <Bar v-if="loaded" :data="chartData" :options="chartOptions" ref="bar" :id="chartId" />

  </div>
</template>

<script>


import { Bar } from 'vue-chartjs';


import {
  Chart as ChartJS,
  CategoryScale,
  LinearScale,
  PointElement,
  BarElement,
  Title,
  Tooltip,
  Legend,
  Filler
} from 'chart.js'



ChartJS.register(
  CategoryScale,
  LinearScale,
  PointElement,
  BarElement,
  Title,
  Tooltip,
  Legend,
  Filler
);
export default {
  props: {
    chartId: {
      type: String,
      default: 'line-chart'
    }
  },
  data() {
    return {
      loaded: false,
      chartFinalOptions: {
        indexAxis: 'y',
        responsive: true,
        scales: {

          x: {
            reverse: true,
            stacked: true,
            position: 'top',
            grid: {
              display: false,
            }
            , ticks: {
              display: true,
              stepSize: 2,
              min: 0,
              max: 23
            }
          },
          y: {
            stacked: true,
            position: "right",
            grid: {

              display: false
            }
            ,
            ticks: {
              display: false
            }
          }
        },
        plugins: {
          datalabels: {

            display: false
          },
          legend: {
            display: false,
          }
        }
      } ,
      chartData: {
        labels: [],
        datasets: []
      },
      chartOptions: null,
      newChart: null,
      foreCastChartData: {
        labels: ['first', 'second', 'third', 'fourth', 'five'],
        datasets:
          [
            {
              label: 'petunia',
              data: [0, 3, 0, 0, 0],
              backgroundColor: "gray"
            },
            {
              label: 'daisy',
              data: [0, 0, 0, 3, 0],
              backgroundColor: "pink"
            },
            {
              label: 'daisy',
              data: [3, 0, 0, 0, 0],
              backgroundColor: "yellow"
            },
            {
              label: 'daisy',
              data: [0, 0, 0, 0, 3],
              backgroundColor: "blue"
            }
          ]
      }
    };
  },
  methods: {


    async fillChart() {

      this.loaded = false
      try {
        this.loaded = true

        await this.$nextTick();
        const ctx = document.getElementById('line-chart').getContext('2d');
        console.log('ctx :: ', ctx);

        const chartold = ChartJS.getChart('line-chart');
        chartold.destroy();

        const imgblue = new Image();
        imgblue.src = require('@/assets/1.png');

        imgblue.onload = () => {
          const fillPatternimgblue = ctx.createPattern(imgblue, 'repeat');
          this.foreCastChartData.datasets[0].backgroundColor = fillPatternimgblue;
        }

        const imgRed = new Image();
        imgRed.src = require('@/assets/2.png');

        imgRed.onload = () => {
          const fillPatternimgRed = ctx.createPattern(imgRed, 'repeat');
          this.foreCastChartData.datasets[1].backgroundColor = fillPatternimgRed;
        }


        const imgyellow = new Image();
        imgyellow.src = require('@/assets/3.png');

        imgyellow.onload = () => {
          const fillPatternimgyellow = ctx.createPattern(imgyellow, 'repeat');
          this.foreCastChartData.datasets[2].backgroundColor = fillPatternimgyellow;
        }

        const imgpink = new Image();
        imgpink.src =  require('@/assets/4.png');

        imgpink.onload = () => {
          const fillPatternimgPink = ctx.createPattern(imgpink, 'repeat');
          this.foreCastChartData.datasets[3].backgroundColor = fillPatternimgPink;
        }


        






        this.newChart = new ChartJS(ctx, {
          type: 'bar',
          data: this.foreCastChartData,
          options:this.chartFinalOptions

        });

        this.newChart.update();

      } catch (e) {
        console.log(e.message);
      }
    },

    sleepy(ms) {
      return new Promise(resolve => setTimeout(resolve, ms));
    }

  }
  , mounted() {
    this.chartOptions = this.chartFinalOptions;
    this.fillChart();


  }

  , components: { Bar }
};


</script>

<style scoped>
button {
  display: inline-block;
  margin-right: 80px;
  justify-content: center;
  border: none;
  height: 30px;
  width: 60px;
  border-radius: 20px;
  cursor: pointer;
  font-size: smaller;
  font-weight: 200;
  color: rgb(192, 186, 186);
  border: non e;

}


button:focus {
  background-color: rgb(217, 227, 227);
  border-radius: 20px;
  font-weight: bold;
  color: rgb(148, 140, 237);
  outline: none;
  /* transition: all 0.10s ease-in-out; */
}


button:hover {
  border-bottom: lightgrey;
  border-bottom-style: solid;
  font-weight: bold;
  color: rgb(148, 140, 237);
  transition: all 0.20s ease-in-out;

}

.bar {

  top: 240px;
  left: 60px;
  position: absolute;
  width: 30%;
  height: 250px;
  /* background-color: yellow; */

}

.lineChart {
  position: absolute;
  width: 100%;
  height: 700px;


}

.yaxis {
  position: relative;
  font-size: smaller;
  top: 85%;
  left: -5%;

}
</style>
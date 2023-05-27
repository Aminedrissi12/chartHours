<template>
  <a-form>
    <div class="CP_chart flexBox">
      <a-form-item :wrapper-col="{ span: 13, offset: 0 }" style="width: 40%">
        <a-select show-search style="width: 200px">
          <div
            v-for="City in Citys"
            :key="City.ville"
            @click="filter(City.ville)"
          >
            <a-select-option></a-select-option>
          </div>
        </a-select>
      </a-form-item>
    </div>
  </a-form>
  <div class="CP_chart" style="">
    <canvas id="myChart"></canvas>
  </div>
</template>

<script>
import dataCity from '../assets/Json/ville.json'
import Chart from 'chart.js/auto'

export default {
  name: 'BarChart',
  data() {
    return {
      Citys: dataCity,
      chartData: null,
      config: {
        type: 'bar',
        data: {
          labels: [
            'January',
            'February',
            'March',
            'April',
            'May',
            'June',
            'July',
            'August',
            'September',
            'October',
            'November',
            'December',
          ],
          datasets: [
            {
              label: 'Hours in monthly',
              backgroundColor: '#f87979',
              data: [],
            },
          ],
        },
        options: {
          responsive: true,
        },
      },
    }
  },
  mounted() {
    let ctx = document.getElementById('myChart').getContext('2d')
    this.chartData = new Chart(ctx, this.config)
    return this.chartData
  },
  methods: {
    filter(vl) {
      let dataCity = this.Citys.filter((el) => el.ville === vl)

      let dataHour = [
        dataCity[0].monthly[0].hour,
        dataCity[0].monthly[1].hour,
        dataCity[0].monthly[2].hour,
        dataCity[0].monthly[3].hour,
        dataCity[0].monthly[4].hour,
        dataCity[0].monthly[5].hour,
        dataCity[0].monthly[6].hour,
        dataCity[0].monthly[7].hour,
        dataCity[0].monthly[8].hour,
        dataCity[0].monthly[9].hour,
        dataCity[0].monthly[10].hour,
        dataCity[0].monthly[11].hour,
      ]

      console.log(dataCity[0].monthly[0].hour)
      // console.log(this.config.data.datasets[0].data)
      // for (let i = 0; i < dataCity[0].monthly.length; i++) {
      //   this.config.data.datasets[0].data.push(dataCity[0].monthly[i].hour)
      // }

      // if (this.config.datasets[0].data.length !== 0) {
      this.drawChart(dataHour)
      // }
    },

    drawChart(vl) {
      if (this.chartData) {
        this.chartData.destroy()
      }

      let ctx = document.getElementById('myChart').getContext('2d')
      this.chartData = new Chart(ctx, {
        type: this.config.type,
        data: {
          labels: [
            'January',
            'February',
            'March',
            'April',
            'May',
            'June',
            'July',
            'August',
            'September',
            'October',
            'November',
            'December',
          ],
          datasets: [
            {
              label: 'Hours in monthly',
              backgroundColor: '#f87979',
              data: vl,
            },
          ],
        },
        options: this.config.options,
      })
    },
  },
}
</script>

<style scoped>
.CP_chart {
  width: 94%;
  padding: 10px;
  margin: 20px;
  border-radius: 16px;
  box-shadow: 0.5rem 1rem 1rem rgba(0, 0, 0, 0.4);
  border: 1px solid #000;
}
.flexBox {
  display: flex;
  flex-direction: row;
  justify-content: center;
}
</style>

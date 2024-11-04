<template>
  <div>
    <h2>Star Growth Chart</h2>
    <!-- Filtros -->
    <div>
      <label>Filtro de Período:</label>
      <select v-model="timeFilter" @change="updateChart">
        <option value="all">Todo o Período</option>
        <option value="30d">Últimos 30 dias</option>
        <option value="6m">Últimos 6 meses</option>
        <option value="1y">Último ano</option>
      </select>
      
      <label>Tipo:</label>
      <select v-model="chartType" @change="updateChart">
        <option value="absolute">Absoluto</option>
        <option value="cumulative">Cumulativo</option>
      </select>
    </div>
    
    <canvas id="starChart"></canvas>
  </div>
</template>

<script>
import { Chart, registerables } from 'chart.js';
import starsData from '../data/thefuck-sample-100.json'; // Importação de dados JSON

Chart.register(...registerables);

export default {
  name: 'StarChart',
  data() {
    return {
      chart: null,
      timeFilter: 'all',
      chartType: 'absolute',
    };
  },
  mounted() {
    this.initializeChart();
  },
  methods: {
    initializeChart() {
      const ctx = document.getElementById('starChart').getContext('2d');
      this.chart = new Chart(ctx, {
        type: 'line',
        data: this.getChartData(),
        options: {
          responsive: true,
          scales: {
            x: {
              type: 'time',
              time: {
                unit: 'month',
              },
            },
            y: {
              beginAtZero: true,
            },
          },
        },
      });
    },
    getChartData() {
      // Processa dados JSON e aplica filtros
      let filteredData = this.applyFilters(starsData);
      
      // Extrair datas e contar número de estrelas
      let labels = filteredData.map((item) => new Date(item.starred_at));
      let data = Array(labels.length).fill(1);

      // Acumular se chartType for 'cumulative'
      if (this.chartType === 'cumulative') {
        data = data.reduce((acc, value, index) => {
          acc.push(value + (acc[index - 1] || 0));
          return acc;
        }, []);
      }

      return {
        labels,
        datasets: [
          {
            label: 'Número de Estrelas',
            data,
            fill: false,
            borderColor: 'blue',
          },
        ],
      };
    },
    applyFilters(data) {
      const now = new Date();
      let filteredData = data;

      if (this.timeFilter === '30d') {
        filteredData = data.filter((item) => new Date(item.starred_at) >= new Date(now.setDate(now.getDate() - 30)));
      } else if (this.timeFilter === '6m') {
        filteredData = data.filter((item) => new Date(item.starred_at) >= new Date(now.setMonth(now.getMonth() - 6)));
      } else if (this.timeFilter === '1y') {
        filteredData = data.filter((item) => new Date(item.starred_at) >= new Date(now.setFullYear(now.getFullYear() - 1)));
      }

      return filteredData;
    },
    updateChart() {
      this.chart.data = this.getChartData();
      this.chart.update();
    },
  },
};
</script>

<style scoped>
/* Estilos específicos do gráfico */
</style>
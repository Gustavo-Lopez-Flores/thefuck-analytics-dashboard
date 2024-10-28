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
      // Filtra e processa os dados do JSON conforme timeFilter e chartType
      let data = starsData; // Implementar filtragem conforme necessário
      return {
        labels: data.map((item) => new Date(item.starred_at)), // Tempo de estrelas
        datasets: [
          {
            label: 'Número de Estrelas',
            data: data.map((item) => item.stars),
            fill: false,
            borderColor: 'blue',
          },
        ],
      };
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
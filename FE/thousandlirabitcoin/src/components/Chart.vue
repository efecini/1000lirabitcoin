<script setup>
import { ref, onMounted } from 'vue';
import { Chart } from 'chart.js/auto';

const chartRef = ref(null);

onMounted(async () => {
  try {
    // Fetch last 1 year of daily BTC/USD prices from CoinGecko
    const response = await fetch(
      'https://api.coingecko.com/api/v3/coins/bitcoin/market_chart?vs_currency=usd&days=365&interval=daily'
    );
    const data = await response.json();

    // Extract dates and prices
    const labels = data.prices.map((p) => new Date(p[0]).toLocaleDateString());
    const prices = data.prices.map((p) => p[1]);

    // Create the Chart.js line chart
    new Chart(chartRef.value, {
      type: 'line',
      data: {
        labels: labels,
        datasets: [
          {
            label: 'Bitcoin/Dolar',
            data: prices,
            borderColor: '#ffffff',
            backgroundColor: 'rgba(255, 255, 255, 0.1)',
            fill: true,
            tension: 0.4,
            pointRadius: 0,
            borderWidth: 1.5,
          },
        ],
      },
      options: {
        responsive: true,
        maintainAspectRatio: true, // Crucial: allows chart to fill container height
        plugins: {
          legend: {
            display: true,
            position: 'top',
          },
          title: {
            display: true,
            text: 'Her gün 1000 liralık bitcoin alıyorum.',
            color: '#ffffff',
            font: { size: 30 },
            padding: 5,
          },
        },
        scales: {
          x: {
            display: true,
            title: { display: true, text: 'Zaman' },
          },
          y: {
            display: true,
            title: { display: true, text: 'Bitcoin' },
            ticks: {
              callback: (value) => '$' + value.toLocaleString(),
            },
          },
        },
      },
    });
  } catch (error) {
    console.error('Error fetching or rendering chart:', error);
    if (chartRef.value) {
      chartRef.value.parentNode.innerHTML =
        '<p class="text-red-500 text-center">Failed to load chart data.</p>';
    }
  }
});
</script>

<template>
  <div class="h-screen flex flex-col bg-black">
    <!-- Navbar stays at the top -->
    <Navbar />

    <!-- Chart takes up all remaining space -->
    <div class="flex-1 p-4 md:p-8">
      <canvas ref="chartRef"></canvas>
    </div>
  </div>
</template>

<style scoped>
/* Ensure the canvas fills its container completely */
canvas {
  width: 100% !important;
  height: 100% !important;
  background-color: black;
}
</style>

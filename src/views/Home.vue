<template>
  <div class="chart-div">
    <PieChart />
  </div>
</template>

<script lang="ts">
import PieChart from '../components/PieChart.vue';

export default {
  name: 'App',
  components: { PieChart }
}
</script>

<style>
@media (min-width: 1024px) {
  .chart-div {
    display: flex;
    justify-content: center;
    align-items: center;
  }
}

.chart-div {
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>

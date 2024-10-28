<template>
  <div id="app">
    <h1>TheFuck Analytics Dashboard</h1>
    <StarChart />
    <UserHighlights />
  </div>
</template>

<script>
import StarChart from './components/StarChart.vue'
import UserHighlights from './components/UserHighlights.vue'

export default {
  components: {
    StarChart,
    UserHighlights
  }
}
</script>
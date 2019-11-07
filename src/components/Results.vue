<template>
  <div class="container">
    <div class="calculator">
      <p>Total Tip: ${{ totalTip }}</p>
      <p>Total Cost: ${{ totalCostWithTip }}</p>
      <p v-if="groupCount > 1">Split Tip: ${{ tipAfterSplit }}</p>
    </div>
  </div>
</template>

<script>

export default {
  props: {
    totalCost: String,
    percentage: String,
    groupCount: String,
  },
  computed: {
    totalTip: function() {
      let tip = Number(this.totalCost) * (Number(this.percentage) / 100);
      if ( isNaN(tip) ) {
        return (0.00).toFixed(2);
      }
      return tip.toFixed(2);
    },
    totalCostWithTip: function() {
      let total = Number(this.totalTip) + Number(this.totalCost);
      if ( isNaN(total) ) {
        return (0.00).toFixed(2);
      }
      return total.toFixed(2);
    },
    tipAfterSplit: function() {
      let split = Number(this.totalTip) / Number(this.groupCount);
      if ( isNaN(split) ) {
        return (0.00).toFixed(2);
      }
      return split.toFixed(2);
    }
  }
}
</script>


<style scoped>
  
</style>
<template>
  <div class="container">
    <div class="calculator" :style="getBorderColor">
      <label for="total-cost">Total Bill</label>
      <input @input="validateTotalBill" v-model="totalCost"  type="text" id="total-cost">
      <span class="warning">{{ costWarning }}</span>
      <label for="percentage">Tip Percentage - {{ percentage }}%</label>
      <input v-model="percentage" type="range" id="percentage" min="0" max="50">
      <label for="party-size">Party Size</label>
      <input @input="validatePartySize" v-model="groupCount" type="number" id="party-size">
      <span class="warning">{{ partyWarning }}</span>
      <Results :totalCost="totalCost" :percentage="percentage" :groupCount="groupCount" />
    </div>
  </div>
</template>

<script>
import Results from './Results.vue';

export default {

  components: {
    Results
  },
  data () {
    return {
      totalCost: '45.24',
      percentage: '20',
      groupCount: '3',
      costWarning: '',
      partyWarning: '',
    }
  },
  computed: {
    getBorderColor: function() {
      let rate = Number(this.percentage) / 25;
      if( rate > 1 ) {
        rate = 1;
      }
      else if (rate < 0) {
        rate = 0;
      }
      let greenPercent = 255 * rate;
      let redPercent = 255 * (1 - rate);

      let color = 'rgb(' + redPercent + ', ' + greenPercent + ', 0)';
      return 'border: 3px solid ' + color;
    }
  },
  methods: {
    validateTotalBill: function() {
      if (this.totalCost.includes('$')) {
        this.costWarning = 'Total Bill should not include \'$\''
      }
      else if (isNaN(this.totalCost)) {
        this.costWarning = 'Total Bill must be a number';
      }
      else {
        this.costWarning = '';
      }
    },
    validatePartySize: function() {
      if (isNaN(this.groupCount)) {
        this.partyWarning = 'Party size must be a number';
      }
      else if (this.groupCount < 1) {
        this.partyWarning = 'Party size must be more than 0';
      }
      else {
        this.partyWarning = '';
      }
    }
  }
}
</script>


<style scoped>
  .calculator {
    padding: 1rem;
    background-image: linear-gradient(to bottom right, rgba(0, 128, 0, 0.3), rgba(0, 0, 255, 0.3));
    background-color: lightblue;
    border-radius: 0.5rem;
    display: flex;
    flex-direction: column;
    max-width: 450px;
    margin: 0 auto;
    align-items: center;
    border: 4px solid green;
  }

  label {
    width: 100%;
    text-align: left;
    max-width: 300px;
    margin: 0 auto 0.1rem;
  }

  input {
    width: 100%;
    max-width: 300px;
    margin: 0 auto;
    border-radius: 0.1rem;
    border: none;
    font-size: 0.8rem;
    padding: 0.2rem 0.3rem;
    box-sizing: border-box;
  }

  .warning {
    margin-bottom: 1rem;
    font-size: 0.8rem;
    color: red;
  }

  button {
    border-radius: 0.1rem;
    border: none;
    padding: 0.4rem 0.6rem;
    box-shadow: 1px 1px 3px rgba(0, 0, 0, 0.35);
    transition: box-shadow 0.15s linear, background-color 0.15s linear;
    background-color: white;
  }

  button:hover {
    box-shadow: 0px 0px 0px rgba(0, 0, 0, 0.35);
    background-color: rgb(197, 232, 255);
  }
</style>
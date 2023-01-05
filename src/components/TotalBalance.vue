<template>
  <div class="total-value" :style="{ color: changeBalanceColor()}">Balance: {{ total }}</div>
</template>

<script>
export default {
  name: 'TotalBalance',
  props: {
    total: {
      type: Number,
      default: 0
    }
  },
  data: () => ({
    balanceColors: {
      Red: '#B25252',
      Black: '#393A3C',
      Green: '#85CE61'
    }
  }),
  methods: {
    changeBalanceColor() {
      return this.total === 0 ? 
        this.balanceColors.Black : this.total > 0 ? 
        this.balanceColors.Green : this.balanceColors.Red;
    }
  }
}
</script>

<style scoped>
.total-value {
  font-size: 26px;
  text-transform: uppercase;
  padding: 20px;
  text-align: center;
}
</style>
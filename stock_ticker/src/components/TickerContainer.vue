<template>
  <div class="ticker-container">
    <div class="ticker-col" v-for="item in tickers" :key="item.symbol">
      <ticker-cell
      :start-val="parseInt(item.startVal).toFixed(2)"
      :daily-max="parseInt(item.dailyMax).toFixed(2)"
      :daily-min="parseInt(item.dailyMin).toFixed(2)"
      :company-name="item.companyName"
      :symbol="item.symbol"
      :delta-val="parseInt(item.deltaVal).toFixed(2)"
      :delta-prcnt="parseInt(item.deltaPrcnt).toFixed(2)"
      :curr-price="item.currPrice"></ticker-cell>
    </div>
  </div>
</template>

<script>
import TickerCell from "./TickerCell.vue";
export default {
  name: "TickerContainer",
  components: {
    TickerCell
  },
  props: {
    tickers: Array
  }
};
</script>
<style lang="scss">
@import "../styles/container.scss";
</style>

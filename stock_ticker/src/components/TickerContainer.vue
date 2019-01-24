<template>
  <div class="ticker-container">
    <ticker-cell
      :start-val="300"
      :daily-max="400"
      :daily-min="200"
      :company-name="'Google'"
      :symbol="'GOOG'"
      :delta="15.32"
      :curr-price="706.32"></ticker-cell>
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

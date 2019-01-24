<template>
  <div class="ticker-cell">
    <div class="cell-left">
      <div class="company-name">{{companyName}}</div>
      <div class="company-symbol">{{symbol}}</div>
      <div class="percent-change">{{delta}}</div>
      <div class="current-price">{{currPrice}}</div>
    </div>
    <div class="cell-right">
      <div class="daily-max">{{dailyMax}}</div>
      <div class="daily-min">{{dailyMin}}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "TickerCell",
  props: [
    "companyName",
    "symbol",
    "dailyMax",
    "dailyMin",
    "delta",
    "currPrice",
    "startVal"
  ]
};
</script>
<style lang="scss">
@import "../styles/cell.scss";
</style>

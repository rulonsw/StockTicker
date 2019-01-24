<template>
  <div class="ticker-cell">
    <div class="cell-left">
      <div class="company-name">{{companyName}}</div>
      <div class="company-symbol">{{symbol}}</div>
      <div class="percent-change">{{delta}}</div>
      <div class="current-price">{{currPrice}}</div>
    </div>
    <div class="cell-right">
        <div class="cell-right-col-0">
            <line-gauge :min=200 :max=400 :ptr=200></line-gauge>
        </div>
        <div class="cell-right-col-1">

      <div class="daily-max">{{dailyMax}}</div>
      <div class="daily-min">{{dailyMin}}</div>
        </div>
    </div>
  </div>
</template>

<script>
import lineGauge from "./LineGauge.vue";
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
  ],
  components: { lineGauge }
};
</script>
<style lang="scss">
@import "../styles/cell.scss";
</style>

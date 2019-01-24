<template>
  <div class="ticker-cell">
    <div class="cell-left">
      <div class="company-name">{{companyName}}</div>
      <div class="company-symbol">{{symbol}}</div>
      <div v-if="isPositive" class="percent-change green-text">
        <span>&#9650;</span>
        ${{deltaVal}} ({{deltaPrcnt}}%)
      </div>
      <div v-else class="percent-change red-text">
        <span>&#9660;</span>
         ${{deltaVal}} ({{deltaPrcnt}}%)
      </div>
      <div class="current-price">${{currPrice}}</div>
    </div>
    <div class="cell-right">
      <div class="cell-right-col-0">
          <line-gauge :min=dailyMin :max=dailyMax :ptr=currPrice></line-gauge>
      </div>
      <div class="cell-right-col-1">
      <div class="daily-max">${{dailyMax}}</div>
      <div class="daily-min">${{dailyMin}}</div>
        </div>
    </div>
  </div>
</template>

<script>
import lineGauge from "./LineGauge.vue";
export default {
  name: "TickerCell",
  props: {
    companyName: String,
    symbol: String,
    dailyMax: Number,
    dailyMin: Number,
    currPrice: Number,
    startVal: Number,
    deltaVal: Number,
    deltaPrcnt: Number
  },
  computed: {
    // positive in terms of outcome (i.e., this stock didn't lose money today). net-zero counts as positive.
    isPositive: function() {
      return this.deltaVal >= 0;
    }
  },
  components: { lineGauge }
};
</script>
<style lang="scss">
@import "../styles/cell.scss";
</style>

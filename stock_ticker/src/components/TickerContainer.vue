<template>
  <div class="ticker-container">
    {{tickers}} <br/>
    <ticker-cell></ticker-cell>
  </div>
</template>

<script>
import TickerCell from "./TickerCell.vue";
export default {
  name: "TickerContainer",
  components: {
    TickerCell
  },
  props: ["tickers"]
};
</script>
<style lang="scss">
@import "../styles/container.scss";
</style>

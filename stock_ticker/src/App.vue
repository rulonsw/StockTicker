<head>

</head>
<template>
  <div id="app">
    <entry-header/>
    <ticker-container :tickers="arrayOfNums" />
  </div>
</template>

<script>
import EntryHeader from "./components/StockEntryHeader.vue";
import TickerContainer from "./components/TickerContainer.vue";

export default {
  name: "app",
  components: {
    EntryHeader,
    TickerContainer
  },
  data: () => {
    return {
      arrayOfNums: [1, 2, 3, 4, 5],
      tickerReqResults: []
    };
  }
};
</script>

<style lang="scss">
@import "styles/main.scss";
</style>

<head>

</head>
<template>
  <div id="app">
    <entry-header v-on:request-accepted="pushToList" v-on:bad-request="badRequest"/>
    <ticker-container :tickers="tickerReqResults" />
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
      tickerReqResults: []
    };
  },
  methods: {
    pushToList: function(obj) {
      this.tickerReqResults.forEach(element => {
        if (element.symbol === obj.symbol) {
          return null;
        }
      });
      return this.tickerReqResults.push(obj);
    },
    badRequest: function() {
      alert(
        "The given symbol is not valid, or AlphaVantage's API response was unexpected.\nPlease try again."
      );
    }
  }
};
</script>

<style lang="scss">
@import "styles/main.scss";
</style>

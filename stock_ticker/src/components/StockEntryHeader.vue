<template>
  <div class="header-elements">
    <header>Stock Watcher</header>
    <input v-model="symbolInput" class="symbol-input" placeholder="Enter stock symbol...">
    <button  
      v-on:click="fetchDailyData(symbolInput)" 
      v-on:keyup.enter="fetchDailyData(symbolInput)" 
      class="add-button">ADD
    </button>
  </div>
</template>

<script>
const axios = require("axios");
const APIKey = "MQ4O4Q71Z6M5Q5TY";
const fun = "GLOBAL_QUOTE";
const apiBaseURL = "https://www.alphavantage.co/query";

const responseBaseObj = "Global Quote";

export default {
  name: "entryHeader",
  data: function() {
    return {
      symbolInput: ""
    };
  },
  methods: {
    fetchDailyData(sym) {
      try {
        return (
          axios
            .get(apiBaseURL, {
              params: {
                function: fun,
                symbol: sym,
                apikey: APIKey
              }
            })
            .then(resp => {
              // eslint-disable-next-line
          // debugger;
              if (Object.keys(resp.data[responseBaseObj]).length !== 0) {
                // Check for rate limiting
                if (resp.data["Note"]) {
                  return alert(
                    "We've hit a rate limit because I can't afford a premium API key. Sorry!"
                  );
                }
                // this was a good request.
                let baseObj = resp.data[responseBaseObj];
                // eslint-disable-next-line
            console.log('here')
                this.$emit("request-accepted", {
                  // company name is not included in quote. I'll have to make another call.
                  companyName: "TODO",
                  symbol: baseObj["01. symbol"],
                  dailyMax: parseInt(baseObj["03. high"]).toFixed(2),
                  dailyMin: parseInt(baseObj["04. low"]).toFixed(2),
                  currPrice: parseInt(baseObj["05. price"]).toFixed(2),
                  startVal: parseInt(baseObj["02. open"]).toFixed(2),
                  deltaVal: parseInt(baseObj["09. change"]).toFixed(2),
                  deltaPrcnt: parseInt(
                    baseObj["10. change percent"].slice(0, -1)
                  ).toFixed(2)
                });
              } else {
                this.$emit("bad-request");
              }
            })
            // eslint-disable-next-line
        .catch(err => console.error(err))
        );
      } catch (err) {
        // eslint-disable-next-line
        console.error(err);
      }
    }
  }
};
</script>

<style lang="scss">
@import "../styles/header.scss";
</style>

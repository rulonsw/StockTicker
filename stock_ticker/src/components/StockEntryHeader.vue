<template>
  <div class="header-elements">
    <header>Stock Watcher</header>
    <input v-model="symbolInput" class="symbol-input" v-on:keyup.enter="fetchDailyData(symbolInput)" placeholder="Enter stock symbol...">
    <button  
      v-on:click="fetchDailyData(symbolInput)" 
      
      class="add-button" :class="{disabled:(symbolInput === '')}">ADD
    </button>
  </div>
</template>

<script>
const axios = require("axios");
const APIKey = "MQ4O4Q71Z6M5Q5TY";
const fun = "GLOBAL_QUOTE";
const funName = "SYMBOL_SEARCH";
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
      if (sym === "") return null;
      this.symbolInput = "";
      try {
        return (
          axios
            .all([
              axios.get(apiBaseURL, {
                params: {
                  function: fun,
                  symbol: sym,
                  apikey: APIKey
                }
              }),
              axios.get(apiBaseURL, {
                params: {
                  function: funName,
                  keywords: sym,
                  apikey: APIKey
                }
              })
            ])
            .then(
              axios.spread((quoteRes, nameRes) => {
                // parse through name-searching response first
                let name;
                let matchingRecord = nameRes.data.bestMatches.find(element => {
                  return element["9. matchScore"] === "1.0000";
                });
                if (matchingRecord !== undefined) {
                  name = matchingRecord["2. name"];
                } else {
                  name = "Not Found";
                }
                // Now, parse through quote data and combine everything together
                if (Object.keys(quoteRes.data[responseBaseObj]).length !== 0) {
                  // Check for rate limiting response key
                  if (quoteRes.data["Note"]) {
                    return alert(
                      "We've hit a rate limit because I can't afford a premium API key. Sorry!"
                    );
                  }
                  // this was a good request.
                  let baseObj = quoteRes.data[responseBaseObj];
                  let retObj = {
                    // company name is not included in quote. I'll have to make another call.
                    companyName: name,
                    symbol: baseObj["01. symbol"],
                    dailyMax: parseFloat(baseObj["03. high"]).toFixed(2),
                    dailyMin: parseFloat(baseObj["04. low"]).toFixed(2),
                    currPrice: parseFloat(baseObj["05. price"]).toFixed(2),
                    startVal: parseFloat(baseObj["02. open"]).toFixed(2),
                    deltaVal: parseFloat(baseObj["09. change"]).toFixed(2),
                    deltaPrcnt: parseFloat(
                      baseObj["10. change percent"].slice(0, -1)
                    ).toFixed(4)
                  };
                  this.$emit("request-accepted", retObj);
                } else {
                  this.$emit("bad-request");
                }
              })
            )
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

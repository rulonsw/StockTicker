<head>

</head>
<template>
  <div id="app">
    <entry-header/>
  </div>
</template>

<script>
import EntryHeader from "./components/StockEntryHeader.vue";

export default {
  name: "app",
  components: {
    EntryHeader
  }
};
</script>

<style lang="scss">
@import "styles/main.scss";
</style>

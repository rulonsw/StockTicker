<head>

</head>
<template>
  <div id="app">
    <entry-header msg="Welcome to Your Vue.js App"/>
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
  @import 'styles/main.scss'
</style>

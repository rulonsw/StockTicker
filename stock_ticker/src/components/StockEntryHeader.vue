<template>
  <div class="header-elements">
    <header>Stock Watcher</header>
    <input v-model="message" placeholder="Enter stock symbol...">
    <button class="add-button">Yo</button>
  </div>
</template>

<script>
export default {
  name: "entryHeader",
  components: {}
};
</script>

<style lang="scss">
	@import '../styles/header.scss'
</style>


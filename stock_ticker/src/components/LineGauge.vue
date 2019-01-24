<template>
  <div class="graph-component">
    <span class="graph-pointer" :style="{marginTop: computePointerPosition() + 'px'}"> &#9654; </span>
    <div class="graph-line"></div>
  </div>
</template>

<script>
export default {
  name: "lineGauge",
  props: ["min", "max", "ptr", "symbol"],
  computed: {},
  methods: {
    computePointerPosition() {
      // Due to the padding of the scale elements, 76px is the "magic number" in terms of aligning
      // our ptr at the bottom.
      // // eslint-disable-next-line
      // debugger;
      let range = this.max - this.min;
      return 76 - ((this.ptr - this.min) / range) * 76;
    }
  }
};
</script>
<style lang="scss">
@import "../styles/gauge.scss";
</style>

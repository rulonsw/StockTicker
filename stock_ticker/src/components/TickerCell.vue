<template>
    <div class="ticker-cell">
        <div class="cell-left">
            <div class="company-name">
                Google
            </div>
            <div class="company-symbol">
                GOOG
            </div>
            <div class="percent-change">
                
            </div>
            <div class="current-price">

            </div>
        </div>
        <div class="cell-right">
            <div class="daily-max">
                $400
            </div>
            <div class="daily-min">
                $200
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name:"TickerCell"
};
</script>
<style lang="scss">
    @import "../styles/cell.scss";
</style>

<template>
    <div>
        <div class="row" v-if="stocks.length">
            <app-stock v-for="(stock, index) in stocks" :key="index" :stock="stock"></app-stock>
        </div>
        <div class="row pd" v-else>
            <h3>You don't have any Stocks!</h3>
        </div>
    </div>
</template>

<style scoped>
    .pd {
        padding: 10px 30px;
    }
</style>

<script>
import {mapGetters} from 'vuex'
import Stock from './Stock.vue'

export default {
    computed: {
        ...mapGetters({
            stocks: 'stockPortfolio'
        }),
    },
    components: {
        appStock: Stock
    }
}
</script>
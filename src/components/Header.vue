<template>
    <nav class="navbar navbar-expand-lg navbar-light bg-light rounded border">
        <router-link to="/" class="navbar-brand"><a class="nav-link">Stock Trader</a></router-link>
        <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNavDropdown" aria-controls="navbarNavDropdown" aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNavDropdown">
            <ul class="navbar-nav mr-auto">
                <router-link to="/portfolio" activeClass="active" class="nav-item" tag="li"><a class="nav-link">Portfolio</a></router-link>
                <router-link to="/stocks" activeClass="active" class="nav-item" tag="li"><a class="nav-link">Stocks</a></router-link>
                <li class="nav-item"><a class="nav-link" @click="endDay">End Day</a></li>
                <li class="nav-item dropdown pointer" @click="isDropdownOpen =!isDropdownOpen">
                    <a class="nav-link dropdown-toggle pointer" id="navbarDropdownMenuLink" role="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
                    Save & Load
                    </a>
                    <div class="dropdown-menu" :class="{show: isDropdownOpen}" aria-labelledby="navbarDropdownMenuLink">
                        <a class="dropdown-item pointer" @click="saveData">Save</a>
                        <a class="dropdown-item pointer" @click="loadData" >Load</a>
                    </div>
                </li>
            </ul>
            <strong class="navbar-text">Funds: {{funds | currency}}</strong>
        </div>
    </nav>
</template>

<script>
import {mapActions} from 'vuex'
export default {
    data() {
        return {
            isDropdownOpen: false
        }
    },
    computed: {
        funds() {
            return this.$store.getters.funds;
        }
    },
    methods: {
        ...mapActions({
            randomizeStocks: 'randomizeStocks',
            fetchData: 'loadData'
        }),
        endDay() {
            this.randomizeStocks();
        },
        saveData() {
            const data = {
                funds: this.$store.getters.funds, 
                stockPortfolio: this.$store.getters.stockPortfolio,
                stocks: this.$store.getters.stocks
            };
            this.$http.put('data.json', data);
        },
        loadData() {
            this.fetchData();
        }
    }
}
</script>

<style scoped>
    .pointer {
        cursor: pointer;
    }
</style>

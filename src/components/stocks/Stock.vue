<template>
    <div class="col-sm-6 pd">
        <div class="card border-success">
            <div class="card-header">
                <h3 class="card-title"> {{ stock.name }} <small>(Price: {{stock.price}} )</small></h3>
            </div>
            <div class="card-body">
                <div class="float-left">
                    <input type="number" class="form-control" placeholder="Quantity" v-model="quantity" :class="{danger: insuficientFunds}">
                </div>
                <div class="float-right">
                    <button class="btn bg-success" @click="buyStock" :disabled="quantity <= 0 || insuficientFunds">{{insuficientFunds ? 'Too Much': 'Buy'}}</button>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
    .pd {
        padding: 10px 30px;
    }
    button {
        color: white;
    }
    .danger {
        border: 1px solid red;
    }
</style>

<script>
export default {
    props: ['stock'],
    data() {
        return {
            quantity: 0
        }
    },
    computed: {
        funds() {
            return this.$store.getters.funds;
        },
        insuficientFunds() {
            return this.quantity * this.stock.price > this.funds;
        }
    },
    methods: {
        buyStock() {
            const order = {
                stockId: this.stock.id,
                stockPrice: this.stock.price,
                quantity: this.quantity
            };
            this.$store.dispatch('buyStock', order);
            this.quantity = 0;
        }
    }
}
</script>

<template>
    <div class="col-sm-6 pd">
        <div class="card border-primary">
            <div class="card-header">
                <h3 class="card-title"> {{ stock.name }} <small>(Price: {{stock.price}} || Quantity: {{stock.quantity}} )</small></h3>
            </div>
            <div class="card-body">
                <div class="float-left">
                    <input type="number" class="form-control" placeholder="Quantity" v-model="quantity" :class="{danger: insuficientQuantity}">
                </div>
                <div class="float-right">
                    <button class="btn bg-success" @click="sellStock" :disabled="quantity <= 0 || insuficientQuantity">{{insuficientQuantity ? 'Not Enough': 'Sell'}}</button>
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
import {mapActions} from 'vuex';

export default {
    props: ['stock'],
    data() {
        return {
            quantity: 0
        }
    },
    computed: {
        insuficientQuantity() {
            return this.quantity > this.stock.quantity;
        }
    },
    methods: {
        ...mapActions({
            placeSellOrder: 'sellStock'
        }),
        sellStock() {
            const order = {
                stockId: this.stock.id,
                stockPrice: this.stock.price,
                quantity: this.quantity
            };
            this.placeSellOrder(order);
            this.quantity = 0;
        }
    }
}
</script>

<template>
  <div class="col-sm-5 card border-primary mb-3" style="display: inline-block; margin-right: 30px;">
    <div class="card-header">
      <h3>
        {{stock.name}}
        <small>(Price: {{stock.price}} | Quantity: {{stock.quantity}})</small>
      </h3>
    </div>
    <div class="card-body text-primary">
      <div class="float-left">
        <input type="number" class="form-control mb-3"
               v-model="quantity"
               placeholder="Quantity"
               :class="{danger: insufficientQuantity}">
      </div>
      <div class="float-right">
        <button class="btn btn-primary"
                @click="sellStock"
                :disabled="insufficientQuantity || quantity <= 0">Sell</button>
      </div>
    </div>
  </div>
</template>

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
      insufficientQuantity() {
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
          quantity:  this.quantity
        };

        this.placeSellOrder(order);
        this.quantity = 0;
      }
    }
  }
</script>

<style scoped>
  .danger {
    border: 1px solid darkred;
  }
</style>


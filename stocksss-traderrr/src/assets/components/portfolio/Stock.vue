<template>
  <div class="col-xl-3 col-lg-3 col-md-6 col-sm-12 col-xs-12 mb-5 mt-4">
    <div class="card">
      <div class="card-header bg-info text-white">
        <h3>
          {{ stock.name }}
          <small>(Price: {{ stock.price }} | Quantity: {{ stock.quantity }})</small>
        </h3>
      </div>
      <div class="card-body ">
        <div class="media">
          <input
            type="number"
            class="form-control"
            placeholder="Quantity"
            v-model="quantity"
            :class="{danger: insufficientQuantity}"
          >
          <div class="media-body">
            <button
              class="btn btn-success ml-2"
              @click="sellStock"
              :disabled="insufficientQuantity || quantity <= 0|| Number.isInteger(quantity)"
            >{{ insufficientQuantity ? "Not enough stocks":"Sell"}}</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

  import {mapActions} from 'vuex';

  export default {
    props:['stock'],
    data(){
      return{
        quantity:0
      }
    },
    computed:{
      insufficientQuantity() {
        return this.quantity > this.stock.quantity;
      }
    },
    methods:{
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

<style scoped>
  .danger{
    border:2px solid red;
  }
</style>

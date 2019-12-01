<template>
    <div class="col-xl-3 col-lg-3 col-md-6 col-sm-12 col-xs-12 mb-5 mt-4">
      <div class="card">
        <div class="card-header">
          <h3>
            {{ stock.name }}
            <small>(Price: {{ stock.price }})</small>
          </h3>
        </div>
        <div class="card-body">
          <div class="media">
            <input
              type="number"
              class="form-control"
              placeholder="Quantity"
              v-model="quantity"
              :class="{danger:insufficientFunds}"
            >
            <div class="media-body">
              <button
                class="btn btn-success ml-2"
                @click="buyStock"
                :disabled="insufficientFunds || quantity <= 0|| Number.isInteger(quantity)"
              >{{ insufficientFunds ? "Insufficient funds": "Buy" }}</button>
            </div>
          </div>
        </div>
      </div>
    </div>
</template>

<script>
    export default {
        props:['stock'],
      data(){
          return{
            quantity:0
          }
      },
      computed:{
        funds(){
          return this.$store.getters.funds;
        },
        insufficientFunds(){
          return this.quantity * this.stock.price > this.funds;
        }
      },
      methods:{
          buyStock(){
            const order = {
              stockId: this.stock.id,
              stockPrice: this.stock.price,
              quantity: this.quantity
            };
            console.log(order);
            this.$store.dispatch('buyStock',order);
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

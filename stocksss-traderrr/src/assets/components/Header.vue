<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <router-link to="/" class="navbar-brand">Stock Trader</router-link>

    <div class="collapse navbar-collapse">
      <ul class="navbar-nav ">
        <router-link to="/portfolio" activeClass="active" tag="li"><a>Portfolio</a></router-link>
        <router-link to="/stocks" activeClass="active" tag="li"><a>Stocks</a></router-link>
      </ul>
      <strong >Funds:  {{funds | currency}}</strong>
      <ul class="nav navbar-nav navbar-right" >
        <li><a href="#" @click="endDay">End Day</a></li>
        <li
          class="dropdown "
          :class="{show: isDropdownOpen}"
          @click="dropdownToggle"
        >
          <a
            href="#"
            class="dropdown-toggle"
            data-toggle="dropdown"
            role="button"
            aria-haspopup="true"
            aria-expanded="false">Save & Load <span class="caret"></span></a>
          <ul class="dropdown-menu">
            <li><a href="#" @click="saveData">Save Data</a></li>
            <li><a href="#" @click="loadData">Load Data</a></li>
          </ul>
        </li>
        <li><a href="#" @click="saveData">Save Data</a></li>
        <li><a href="#" @click="loadData">Load Data</a></li>
      </ul>
    </div>
  </nav>
</template>

<script>

    import {mapActions} from 'vuex';

    export default {
      data(){
        return {
            isDropdownOpen: false
          }
        },
      computed:{
          funds(){
            return this.$store.getters.funds;
          }
        },
      methods:{
        ...mapActions({
            randomizeStocks:'randomizeStocks',
            fetchData:'loadData'
        }),
        endDay(){
            this.randomizeStocks();
        },
        dropdownToggle(){
            this.isDropdownOpen =! this.isDropdownOpen;
        },
        saveData(){
            const data = {
              funds: this.$store.getters.funds,
              stockPortfolio:this.$store.getters.stockPortfolio,
              stocks:this.$store.getters.stocks
              };
            this.$http.put('data.json',data);
        },
        loadData(){
          this.fetchData();
        }

      }
    }
</script>

<style scoped>
  li{
    padding-left:50px;
  }
  strong{
    padding: 0 20px 0 80px;
  }
</style>

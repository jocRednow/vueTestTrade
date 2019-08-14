<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-light mb-5">
    <router-link class="navbar-brand mb-0 h1" to="/">Stock Trader</router-link>
    <div class="collapse navbar-collapse">
      <ul class="navbar-nav mr-auto">
        <router-link class="nav-item" tag="li" activeClass="active"
                     to="/portfolio"><a class="nav-link">Portfolio</a></router-link>
        <router-link class="nav-item" tag="li" activeClass="active"
                     to="/stocks"><a class="nav-link">Stocks</a></router-link>
      </ul>
      <ul class="navbar-nav my-2 my-lg-0">
        <li><a href="#" class="nav-link" @click="endDay">End Day</a></li>
        <li class="nav-item dropdown">
          <a class="nav-link dropdown-toggle" href="#"
             id="navbarDropdown" role="button" data-toggle="dropdown"
             aria-haspopup="true" aria-expanded="false">
            Save & Load
          </a>
          <div class="dropdown-menu" aria-labelledby="navbarDropdown">
            <a class="dropdown-item" href="#" @click="saveData">Save Data</a>
            <a class="dropdown-item" href="#" @click="loadData">Load Data</a>
          </div>
        </li>
        <strong class="nav-link">Funds: {{ funds | currency }}</strong>
      </ul>
    </div>
  </nav>
</template>

<script>
  import {mapActions} from 'vuex';

  export default {
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

</style>

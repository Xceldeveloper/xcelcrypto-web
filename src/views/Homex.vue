<template>
  <div id="coverx">
    <navbar />

    <newslist />

    <currencieslist />
  </div>
</template>

<script>
import currencieslist from "../components/currencieslist.vue";
import navbar from "../components/nav.vue";
import newslist from "../components/newslist.vue";

const CoinGecko = require("coingecko-api");

const CoinGeckoClient = new CoinGecko();

export default {
  name: "Homex",
  components: { currencieslist, navbar, newslist },
  data() {
    return {
     
    };
  },
};
</script>

<style scoped>

</style>
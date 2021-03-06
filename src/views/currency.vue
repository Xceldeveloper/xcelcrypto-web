<template>
  <div>
   
    {{data.data.market_data.price_change_percentage_24h.toFixed(2)}}
    <br />
    <br />
    {{ data }}
  </div>
</template>

<script>
const CoinGecko = require("coingecko-api");

const CoinGeckoClient = new CoinGecko();
export default {
  data() {
    return {
      currency: "",
      data: "",
    };
  },
  mounted() {
      this.currency = this.$route.query.name
      console.log(this.currency)

        this.getDetails();

  },
  methods: {
    async getDetails() {
      let datax = await CoinGeckoClient.coins.fetch('bitcoin', {});
      this.data = datax
      console.log(JSON.stringify(this.data,2,null))
    },
  },
};
</script>

<style>
</style>
<template>
  <div>
   
    {{Object.keys(data.data.market_data)}}
    <br />
    <br />
    {{ data.data.market_data.ath.usd}}
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
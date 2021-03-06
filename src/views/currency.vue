<template>
  <div>
    {{ currency }}
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
      this.currency = this.$route.params.name
    this.getDetails();
  },
  methods: {
    async getDetails() {
      this.data = await CoinGeckoClient.coins.fetch(this.currency, {});
    },
  },
};
</script>

<style>
</style>
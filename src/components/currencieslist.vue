<template>
  <div id="wrapper" v-if="currencies.length > 0">
    <table id="tablex">
      <thead class="bg-white">
        <tr>
          <th class="w-1/4 xyz">Name</th>
          <th class="w-1/4 xyz">Price</th>
          <th class="w-1/4 xyz">24h</th>
          <th class="w-1/4 xyz">Market Cap</th>
        </tr>
      </thead>
      <tbody class="bg-white divide-y divide-gray-200">
        <tr v-for="(currency, index) in currencies" :key="index" >
          <td class="px-6 py-4 whitespace-nowrap" v-if="index <= 29">
            <div class="flex items-center">
              <div class="flex-shrink-0 h-10 w-10">
                <img
                  id="logox"
                  :src="currency.image.thumb"
                  :alt="currency.name"
                />
              </div>
              <div class="ml-4">
                <div class="text-sm font-medium text-gray-900">
                  {{ currency.name }}
                </div>
                <div class="text-sm text-left text-gray-500">
                  {{ currency.symbol }}
                </div>
              </div>
            </div>
          </td>
          <td class="px-6 py-4 whitespace-nowrap" v-if="index <= 29">
            <div class="text-sm text-gray-900">
              {{ formatCurrency(currency.market_data.current_price.usd) }}
            </div>
          </td>
          <td class="px-6 py-4 whitespace-nowrap" v-if="index <= 29">
            <div class="ml-4 content-center">
              <div
                class="text-sm text-center font-medium text-gray-900"
                v-html="percentages[index]"
              ></div>
            </div>
          </td>
          <td class="px-6 py-4 whitespace-nowrap" v-if="index <= 29">
            <div class="text-sm text-gray-900">
              {{ formatCurrency(currency.market_data.market_cap.usd) }}
            </div>
          </td>
        </tr>

        <!-- More items... -->
      </tbody>
    </table>
  </div>
</template>

<script>
const CoinGecko = require("coingecko-api");

const CoinGeckoClient = new CoinGecko();
import axios from "axios";

export default {
  data() {
    return {
      currencies: [],
      currenciesx: [],
      percentages: [],
    };
  },
  mounted() {
    // axios.get('https://api.coingecko.com/api/v3/coins/markets?vs_currency=usd&ids=dogecoin').then(res=>{
    //   this.currencies = res
    //   console.log(res)
    // }).catch(error=>{
    //   console.log(error);
    // })
    this.getCurrencies();
  },

  methods: {
    async getCurrencies() {
      this.currenciesx = await CoinGeckoClient.coins.all();
      this.currencies = this.currenciesx.data;
    },

    formatCurrency(value, currency = "USD", lang = "en-US") {
      return new Intl.NumberFormat(lang, {
        style: "currency",
        currency: currency,
      }).format(value);
    },

    async percentageData(index) {
      let res = await CoinGeckoClient.coins.fetch(
        this.currencies[index].name.toLowerCase(),
        {}
      );
      var rox =
        res.data.market_data.price_change_percentage_24h.toFixed(2) + "";

      if (rox.indexOf("-") > -1) {
        this.percentages.splice(
          index,
          0,
          '<span style="color:red">' + rox + "%</span>"
        );
      } else {
        this.percentages.splice(
          index,
          0,
          '<span style="color:green">' + "+" + rox + "%</span>"
        );
      }
    },
  },
  watch: {
    currencies(val) {
      if (val.length == 50) {
        console.log("ready");
        for (var i = 0; i < val.length; i++) {
          this.percentageData(i);
        }
      }
    },
  },
};
</script>

<style scoped>
#wrapper {
  width: 100vw;

  overflow: auto;
}
#tablex {
  width: 100%;
  max-width: 900px;
  display: block;
  margin: 20px auto;
  box-shadow: 0px 2px 10px lightgrey;
}

.xyz {
  padding: 10px;
}
</style>
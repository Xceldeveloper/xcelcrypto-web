<template>
 <div id="wrapper" v-if="currencies.length > 0">
      <table
    id="tablex"
   
  >
    <thead class="bg-white ">
      <tr>
        <th class="w-1/4 xyz">Name</th>
        <th class="w-1/4 xyz">Price</th>
        <th class="w-1/4 xyz">24h</th>
        <th class="w-1/4 xyz">Market Cap</th>
      </tr>
    </thead>
    <tbody class="bg-white divide-y divide-gray-200">
      <tr v-for="currency in currencies" :key="currency.id">
        <td class="px-6 py-4 whitespace-nowrap">
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
        <td class="px-6 py-4 whitespace-nowrap">
          <div class="text-sm text-gray-900">
            {{ formatCurrency(currency.market_data.current_price.usd) }}
          </div>
        </td>
        <td class="px-6 py-4 whitespace-nowrap">
          <div class="ml-4 content-center">
            <div class="text-sm text-center font-medium text-gray-900">40%</div>
            <div class="content-center text-gray-500">
              <svg
                class="w-6 h-6 mr-2 text-red-500 fill-current"
                fill="current"
                stroke="currentColor"
                viewBox="0 0 24 24"
                xmlns="http://www.w3.org/2000/svg"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M13 17h8m0 0V9m0 8l-8-8-4 4-6-6"
                ></path>
              </svg>
            </div>
          </div>
        </td>
        <td class="px-6 py-4 whitespace-nowrap">
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

export default {
  data() {
    return {
      currencies: [],
      currenciesx: [],
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

    
  },
};
</script>

<style scoped>
#wrapper{
  width: 100vw;
  
  overflow: auto;

}
#tablex {
  width: 100%;
  max-width: 900px;
  display: block;
  margin:20px auto;
    box-shadow: 0px 2px 10px lightgrey;
}


.xyz{
  padding: 10px;
}
</style>
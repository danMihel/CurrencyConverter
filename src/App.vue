<template>
  <div id="app" class="container">
    <h1 class="text-center py-2">Currency conversion</h1>
    <p class="fs-5" id="baseValue">1 {{ currencyInput }} = {{ rate }} {{ currencyOutput }}</p>
    <div class="row">
      <div class="col">
        <button class="btn btn-light m-1" name="usd" id="usd" @click="currentInput('RUB')">RUB</button>
        <button class="btn btn-light m-1" name="usd" id="usd" @click="currentInput('USD')">USD</button>
        <button class="btn btn-light m-1" name="usd" id="usd" @click="currentInput('EUR')">EUR</button>
        <button class="btn btn-light m-1" name="usd" id="usd" @click="currentInput('GBP')">GBP</button>
        <select class="form-select text-center" name="first-currency" id="first-currency" @change="calculateResults()"
          value="" v-model="currencyInput">
          <option value="AED">AED</option>
          <option value="ARS">ARS</option>
          <option value="AUD">AUD</option>
          <option value="BGN">BGN</option>
          <option value="BRL">BRL</option>
          <option value="BSD">BSD</option>
          <option value="CAD">CAD</option>
          <option value="CHF">CHF</option>
          <option value="CLP">CLP</option>
          <option value="CNY">CNY</option>
          <option value="COP">COP</option>
          <option value="CZK">CZK</option>
          <option value="DKK">DKK</option>
          <option value="DOP">DOP</option>
          <option value="EGP">EGP</option>
          <option value="EUR">EUR</option>
          <option value="FJD">FJD</option>
          <option value="GBP">GBP</option>
          <option value="GTQ">GTQ</option>
          <option value="HKD">HKD</option>
          <option value="HRK">HRK</option>
          <option value="HUF">HUF</option>
          <option value="IDR">IDR</option>
          <option value="ILS">ILS</option>
          <option value="INR">INR</option>
          <option value="ISK">ISK</option>
          <option value="JPY">JPY</option>
          <option value="KRW">KRW</option>
          <option value="KZT">KZT</option>
          <option value="MXN">MXN</option>
          <option value="MYR">MYR</option>
          <option value="NOK">NOK</option>
          <option value="NZD">NZD</option>
          <option value="PAB">PAB</option>
          <option value="PEN">PEN</option>
          <option value="PHP">PHP</option>
          <option value="PKR">PKR</option>
          <option value="PLN">PLN</option>
          <option value="PYG">PYG</option>
          <option value="RON">RON</option>
          <option value="RUB">RUB</option>
          <option value="SAR">SAR</option>
          <option value="SEK">SEK</option>
          <option value="SGD">SGD</option>
          <option value="THB">THB</option>
          <option value="TRY">TRY</option>
          <option value="TWD">TWD</option>
          <option value="UAH">UAH</option>
          <option value="USD">USD</option>
          <option value="UYU">UYU</option>
          <option value="VND">VND</option>
          <option value="ZAR">ZAR</option>
        </select>
        <input type="number" name="input-one" id="input-one" class="fs-3 p-5 form-control" v-model="amountOne"
          @input="calculateResults()" />
      </div>
      <div class="col d-flex justify-content-center align-items-center">
        <svg xmlns="http://www.w3.org/2000/svg" width="60" height="60" fill="currentColor"
          class="bi bi-arrow-left-right" viewBox="0 0 16 16">
          <path fill-rule="evenodd"
            d="M1 11.5a.5.5 0 0 0 .5.5h11.793l-3.147 3.146a.5.5 0 0 0 .708.708l4-4a.5.5 0 0 0 0-.708l-4-4a.5.5 0 0 0-.708.708L13.293 11H1.5a.5.5 0 0 0-.5.5zm14-7a.5.5 0 0 1-.5.5H2.707l3.147 3.146a.5.5 0 1 1-.708.708l-4-4a.5.5 0 0 1 0-.708l4-4a.5.5 0 1 1 .708.708L2.707 4H14.5a.5.5 0 0 1 .5.5z" />
        </svg>
      </div>
      <div class="col">
        <button class="btn btn-light m-1" name="usd" id="usd" @click="currentOutput('RUB')">RUB</button>
        <button class="btn btn-light m-1" name="usd" id="usd" @click="currentOutput('USD')">USD</button>
        <button class="btn btn-light m-1" name="usd" id="usd" @click="currentOutput('EUR')">EUR</button>
        <button class="btn btn-light m-1" name="usd" id="usd" @click="currentOutput('GBP')">GBP</button>
        <select id="currency-two" class="form-select text-center" @change="calculateResults()" v-model="currencyOutput">
          <option value="AED">AED</option>
          <option value="ARS">ARS</option>
          <option value="AUD">AUD</option>
          <option value="BGN">BGN</option>
          <option value="BRL">BRL</option>
          <option value="BSD">BSD</option>
          <option value="CAD">CAD</option>
          <option value="CHF">CHF</option>
          <option value="CLP">CLP</option>
          <option value="CNY">CNY</option>
          <option value="COP">COP</option>
          <option value="CZK">CZK</option>
          <option value="DKK">DKK</option>
          <option value="DOP">DOP</option>
          <option value="EGP">EGP</option>
          <option value="EUR">EUR</option>
          <option value="FJD">FJD</option>
          <option value="GBP">GBP</option>
          <option value="GTQ">GTQ</option>
          <option value="HKD">HKD</option>
          <option value="HRK">HRK</option>
          <option value="HUF">HUF</option>
          <option value="IDR">IDR</option>
          <option value="ILS">ILS</option>
          <option value="INR">INR</option>
          <option value="ISK">ISK</option>
          <option value="JPY">JPY</option>
          <option value="KRW">KRW</option>
          <option value="KZT">KZT</option>
          <option value="MXN">MXN</option>
          <option value="MYR">MYR</option>
          <option value="NOK">NOK</option>
          <option value="NZD">NZD</option>
          <option value="PAB">PAB</option>
          <option value="PEN">PEN</option>
          <option value="PHP">PHP</option>
          <option value="PKR">PKR</option>
          <option value="PLN">PLN</option>
          <option value="PYG">PYG</option>
          <option value="RON">RON</option>
          <option value="RUB">RUB</option>
          <option value="SAR">SAR</option>
          <option value="SEK">SEK</option>
          <option value="SGD">SGD</option>
          <option value="THB">THB</option>
          <option value="TRY">TRY</option>
          <option value="TWD">TWD</option>
          <option value="UAH">UAH</option>
          <option value="USD">USD</option>
          <option value="UYU">UYU</option>
          <option value="VND">VND</option>
          <option value="ZAR">ZAR</option>
        </select>
        <input class="fs-2 p-5 form-control" type="number" id="amount-two" placeholder="0" v-model="amountTwo" disabled />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  components: {},
  data() {
    return {
      data: [],
      currencyInput: "USD",
      currencyOutput: "EUR",
      rate: 0,
      amountOne: 1,
      amountTwo: 0,
    };
  },

  methods: {
    getLang() {
      if (navigator.language == "ru-RU") {
        this.currencyInput = "RUB"
      }
      if (navigator.language == "en-En") {
        this.currencyInput = "EUR"
      }
      if (navigator.language == "en-US") {
        this.currencyInput = "USD" 
      }
            if (navigator.language == "zh-CN") {
        this.currencyInput = "CNY"
      }
    },
    currentInput(val) {
      this.currencyInput = val;
      this.calculateResults()
    },
    currentOutput(val) {
      this.currencyOutput = val;
      this.calculateResults()
    },
    calculateResults() {
      console.log('fetch')
      fetch(
        `https://v6.exchangerate-api.com/v6/aa2a5d8789b9d2579997c2db/latest/${this.currencyInput
        }`
      )
        .then((res) => res.json())
        .then((data) => {
          this.data = data;
          this.rate = data.conversion_rates[this.currencyOutput];
          const r = this.amountOne * this.rate;
          this.amountTwo = r.toFixed(2);
        });
    },
  },
  mounted() {
    this.calculateResults();
    this.getLang();
  },
};
</script>

<style>
input[type="number"]::-webkit-outer-spin-button,
input[type="number"]::-webkit-inner-spin-button {
    -webkit-appearance: none;
}

input[type='number'],
input[type="number"]:hover,
input[type="number"]:focus {
    appearance: none;
    -moz-appearance: textfield;
}
</style>
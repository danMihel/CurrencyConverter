<template>
  <div id="app" class="container">
    <h1 class="text-center py-2">Currency conversion</h1>
    <p class="fs-5" id="baseValue">
      1 {{ currencyInput }} = {{ rate }} {{ currencyOutput }}
    </p>
    <div class="row flex-md-row flex-column">
      <div class="col">
        <button
          class="btn btn-light m-1"
          name="usd"
          id="RUB"
          @click="currentInput('RUB')"
        >
          RUB
        </button>
        <button
          class="btn btn-light m-1"
          name="usd"
          id="USD"
          @click="currentInput('USD')"
        >
          USD
        </button>
        <button
          class="btn btn-light m-1"
          name="usd"
          id="EUR"
          @click="currentInput('EUR')"
        >
          EUR
        </button>
        <button
          class="btn btn-light m-1"
          name="usd"
          id="GBP"
          @click="currentInput('GBP')"
        >
          GBP
        </button>
        <select
          class="form-select text-center"
          name="first-currency"
          id="first-currency"
          @change="calculateResults()"
          value=""
          v-model="currencyInput"
        >
          <option v-for="option in options" :key="option" :value="option">
            {{ option }}
          </option>
        </select>
        <input
          type="number"
          name="input-one"
          id="input-one"
          class="fs-3 p-5 form-control"
          v-model="amountOne"
          @input="calculateResults()"
        />
      </div>
      <div class="col d-flex justify-content-center align-items-center py-2">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="60"
          height="60"
          fill="currentColor"
          class="bi bi-arrow-left-right"
          viewBox="0 0 16 16"
        >
          <path
            fill-rule="evenodd"
            d="M1 11.5a.5.5 0 0 0 .5.5h11.793l-3.147 3.146a.5.5 0 0 0 .708.708l4-4a.5.5 0 0 0 0-.708l-4-4a.5.5 0 0 0-.708.708L13.293 11H1.5a.5.5 0 0 0-.5.5zm14-7a.5.5 0 0 1-.5.5H2.707l3.147 3.146a.5.5 0 1 1-.708.708l-4-4a.5.5 0 0 1 0-.708l4-4a.5.5 0 1 1 .708.708L2.707 4H14.5a.5.5 0 0 1 .5.5z"
          />
        </svg>
      </div>
      <div class="col">
        <button
          class="btn btn-light m-1"
          name="usd"
          id="RUB2"
          @click="currentOutput('RUB')"
        >
          RUB
        </button>
        <button
          class="btn btn-light m-1"
          name="usd"
          id="USD2"
          @click="currentOutput('USD')"
        >
          USD
        </button>
        <button
          class="btn btn-light m-1"
          name="usd"
          id="EUR2"
          @click="currentOutput('EUR')"
        >
          EUR
        </button>
        <button
          class="btn btn-light m-1"
          name="usd"
          id="GBP2"
          @click="currentOutput('GBP')"
        >
          GBP
        </button>
        <select
          id="currency-two"
          class="form-select text-center"
          @change="calculateResults()"
          v-model="currencyOutput"
        >
          <option v-for="option in options" :key="option" :value="option">
            {{ option }}
          </option>
        </select>
        <input
          class="fs-2 p-5 form-control"
          type="number"
          id="amount-two"
          placeholder="0"
          v-model="amountTwo"
          disabled
        />
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
      options: [
        "AED",
        "ARS",
        "AUD",
        "BGN",
        "BRL",
        "BSD",
        "CAD",
        "CHF",
        "CLP",
        "CNY",
        "COP",
        "CZK",
        "DKK",
        "DOP",
        "EGP",
        "EUR",
        "FJD",
        "GBP",
        "GTQ",
        "HKD",
        "HRK",
        "HUF",
        "IDR",
        "ILS",
        "INR",
        "ISK",
        "JPY",
        "KRW",
        "KZT",
        "MXN",
        "MYR",
        "NOK",
        "NZD",
        "PAB",
        "PEN",
        "PHP",
        "PKR",
        "PLN",
        "PYG",
        "RON",
        "RUB",
        "SAR",
        "SEK",
        "SGD",
        "THB",
        "TRY",
        "TWD",
        "UAH",
        "USD",
        "UYU",
        "VND",
        "ZAR",
      ],
    };
  },

  methods: {
    getLang() {
      if (navigator.language == "ru-RU") {
        this.currencyInput = "RUB";
      }
      if (navigator.language == "en-En") {
        this.currencyInput = "EUR";
      }
      if (navigator.language == "en-US") {
        this.currencyInput = "USD";
      }
      if (navigator.language == "zh-CN") {
        this.currencyInput = "CNY";
      }
    },
    currentInput(val) {
      this.currencyInput = val;
      this.calculateResults();
    },
    currentOutput(val) {
      this.currencyOutput = val;
      this.calculateResults();
    },
    calculateResults() {
      fetch(
        `https://v6.exchangerate-api.com/v6/aa2a5d8789b9d2579997c2db/latest/${this.currencyInput}`
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
    this.getLang();
    this.calculateResults();
  },
};
</script>

<style>
input[type="number"]::-webkit-outer-spin-button,
input[type="number"]::-webkit-inner-spin-button {
  -webkit-appearance: none;
}

input[type="number"],
input[type="number"]:hover,
input[type="number"]:focus {
  appearance: none;
  -moz-appearance: textfield;
}
</style>

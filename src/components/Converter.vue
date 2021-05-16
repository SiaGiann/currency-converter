<template>
  <div class="bg-white text-black p-24 mx-auto w-2/3 rounded-xl shadow-lg mt-16">
    <div class="flex">
      <div class="w-full">
        <label class="block text-gray-700 text-sm font-bold mb-2" for="amount">
          Amount
        </label>
        <input class="input" type="text" v-model.number="amount1" id="amount">
      </div>
      <div class="relative ml-8 w-full">
        <label class="block text-gray-700 text-sm font-bold mb-2" for="from">
          From
        </label>
        <select class="input w-full" v-model="currency1" id="from">
          <option :value="cur" v-for="cur in currencyList" :key="cur">{{ cur }}</option>
        </select>
        <div class="pointer-events-none absolute inset-y-0 right-0 flex items-end mb-2 px-2 text-gray-700">
          <svg class="fill-current h-6 w-6" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20"><path d="M9.293 12.95l.707.707L15.657 8l-1.414-1.414L10 10.828 5.757 6.586 4.343 8z"/></svg>
        </div>
      </div>
    </div>
    <div class="flex my-8">
      <div  class="w-full">
        <label class="block text-gray-700 text-sm font-bold mb-2" for="result">
          Result
        </label>
        <input class="input bg-gray-300" type="text" v-model.number="amount2" id="result" disabled>
      </div>
      <div class="relative ml-8 w-full">
        <label class="block text-gray-700 text-sm font-bold mb-2" for="to">
          To
        </label>
        <select class="input w-full" v-model="currency2" id="to">
          <option :value="cur" v-for="cur in currencyList" :key="cur">{{ cur }}</option>
        </select>
        <div class="pointer-events-none absolute inset-y-0 right-0 flex items-end mb-2 px-2 text-gray-700">
          <svg class="fill-current h-6 w-6" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20"><path d="M9.293 12.95l.707.707L15.657 8l-1.414-1.414L10 10.828 5.757 6.586 4.343 8z"/></svg>
        </div>
      </div>
    </div>
    <button class="button" @click="convertCurrency">Convert</button>
  </div>
</template>

<script>
export default {
  name: "Converter",

  data() {
    return {
      amount1: 1,
      amount2: 1,
      currency1: "EUR",
      currency2: "USD",
      rates: {},
    }
  },

  mounted() {
    this.getRatesFromApi()
  },

  computed: {
    currencyList() {
      return Object.keys(this.rates)
    }
  },

  methods: {
    getRatesFromApi() {
      const url = "http://data.fixer.io/api/latest?access_key=741f1eb0acccfacf0da017d812c6d265&format=1"

      fetch(url)
        .then(response => response.json())
        .then(data => {
          this.rates = data.rates
          this.convertCurrency()
        })
    },

    getModifier(from, to) {
      if (from == to) {
        return 1
      }
      if (from == "EUR") {
        return this.rates[to]
      }
      if (to == "EUR") {
        return 1 / this.rates[from]
      }
      return this.rates[to] / this.rates[from]
    },

    convertCurrency() {
      const modifier = this.getModifier(this.currency1, this.currency2)
      this.amount2 = this.amount1 * modifier
    }
  }
}
</script>

<style scoped>
.input {
  @apply shadow appearance-none border rounded py-2 px-3 text-gray-700 leading-tight;
}

.button {
  @apply bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded;
}
</style>
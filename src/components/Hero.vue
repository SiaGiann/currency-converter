<template>
  <div class="relative bg-green-500 h-96">
    <div class="absolute inset-0">
      <div class="flex mt-20 w-max mx-auto">
        <img class="w-10" :src="currency"/>
        <div class="text-black ml-6 text-5xl font-bold whitespace-nowrap">
          Currency Converter
        </div>
      </div>
      <Converter></Converter>
    </div>
  </div>
</template>

<script>
import Converter from "./Converter.vue";
import currency from "../assets/currency.svg";

export default {
  name: "Hero",

  components: {
    Converter,
  },

  data() {
    return {
      currency
    }
  },
}
</script>

<style scoped>

</style>